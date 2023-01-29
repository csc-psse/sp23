# Lab 11 : Game files

## Entities

### entity

`````` {tab-set}
````` {tab-item} Entity.cpp
``` {code-block} cpp
#include "Entity.hpp"
#include "../items/Item.hpp"

Entity::Entity(std::string name, int health, int damage){
    this->name = name;
    this->health = health;
    this->damage = damage;
}

std::string Entity::getName() {
	return this->name;
}

int Entity::getHealth() {
	return this->health;
}

void Entity::getInfo(){
    std::cout << this->name <<
        "\nHealth: " << this->health << std::endl;
}

Item* Entity::takeDamage(int amount){
    this->health -= amount;

	if (this->health <= 0) {
		std::cout << this->name << " slain!\n";
		return Item::generateRandomItem();
	}

	return nullptr;
}

void Entity::heal(int amount) {
	this->health += amount;
}

Item* Entity::attack(Entity* target){

	std::cout << this->name << " attacks " << target->getName() << " for " << this->damage << "!\n~~~~~\n";

    return target->takeDamage(this->damage);
}

void Entity::displayInventory(){
	this->inventory.displayInventory();
}

void Entity::addItem(Item* item){
	this->inventory.addItem(item);
}

void Entity::useItem(std::string name, Entity* target) {
	this->inventory.useItem(name, target);
}

void Entity::useItem(int index, Entity* target) {
	this->inventory.useItem(index, target);
}

int Entity::getInventorySize() {
	return this->inventory.getSize();
}
```
`````
````` {tab-item} Entity.hpp
``` {code-block} cpp
#pragma once
#include <iostream>
#include <string>
#include "../items/Inventory.hpp"

class Entity{
    private:
        std::string name;
		int health;
        int damage;
		Inventory inventory;
    public:
        Entity(std::string name, int health, int damage);

		std::string getName();
		int getHealth();
        void getInfo();

        Item* takeDamage(int amount);
		void heal(int amount);
        Item* attack(Entity* target);

        void displayInventory();
        void addItem(Item* item);
		void useItem(std::string name, Entity* target);
		void useItem(int index, Entity* target);
		int getInventorySize();
};
```
`````
``````

## Items

### Grenade

`````` {tab-set}
````` {tab-item} Grenade.cpp
``` {code-block} cpp
#include "Grenade.hpp"

Grenade::Grenade() : Item("Grenade", 20) {

}

void Grenade::activate(Entity* target) {
	target->takeDamage(this->power);
}
```
`````
````` {tab-item} Grenade.hpp
``` {code-block} cpp
#pragma once

#include "Item.hpp"

class Grenade : public Item
{

    private:


    public:
        Grenade();
        void activate(Entity* target);
};
```
`````
``````

### Inventory

`````` {tab-set}
````` {tab-item} Inventory.cpp
``` {code-block} cpp
#include "Inventory.hpp"
#include "Item.hpp"

void Inventory::displayInventory() {
	if (this->inventory.size() == 0) {
		std::cout << "Inventory is empty!" << std::endl;
		return;
	}

	for (std::vector<Item*>::iterator it = this->inventory.begin(); it != this->inventory.end(); ++it) {
		std::cout << (*it)->getName() << std::endl;
	}
}

void Inventory::addItem(Item* item) {
	std::cout << "Added " << item->getName() << " to inventory!\n";
	this->inventory.push_back(item);
}

void Inventory::useItem(std::string name, Entity* target) {
	for (unsigned int i = 0; i < this->inventory.size(); i++) {
		if (inventory.at(i)->getName() == name) {
			std::cout << "Used " << name << " on " << target->getName() <<"!\n";
			inventory.at(i)->activate(target);
			inventory.erase(inventory.begin() + i);
		}
	}
}

void Inventory::useItem(int index, Entity* target) {
	inventory.at(index)->activate(target);
	std::cout << "Used " << inventory.at(index)->getName() << " on " << target->getName() << "!\n";
	inventory.erase(inventory.begin() + index);
}

int Inventory::getSize() {
	return this->inventory.size();
}
```
`````
````` {tab-item} Inventory.hpp
``` {code-block} cpp
#pragma once

#include <iostream>
#include <vector>

// Forward declaration.
// Cannot include 'Item', as 'Item' includes 'Entity' & that would cause a circular dependency (compiler would crash with many, many errors.)
// This allows 'Entity' to *know* that 'Item' exists, but *not* how to use it.
class Item;
class Entity;

class Inventory
{
private:
	std::vector<Item*> inventory;
public:
	void displayInventory();
	void addItem(Item* item);
	void useItem(std::string name, Entity* target);
	void useItem(int index, Entity* target);
	int getSize();
};
```
`````
``````

### Item

`````` {tab-set}
````` {tab-item} Item.cpp
``` {code-block} cpp
#include "Item.hpp"
#include "Potion.hpp"
#include "MegaPotion.hpp"
#include "Grenade.hpp"

Item::Item(std::string name, int power) {
	this->name = name;
	this->power = power;
}

std::string Item::getName() {
	return this->name;
}


// This is a factory design pattern. This allows us to create Items during the runtime of the program without them being predetermined
// at compile time.
// We create an `Item pointer` (Item *) in the location we wish to store "some item", then when it comes time to
// create an Item we can use one of the following two functions to either generate a specific Item OR a random Item.
// We can see this play out in the `Inventory` class.
// `Inventory` holds a vector of `Item *`. When an enemy is slain, an Item is randomly generated and stored in the Player's Inventory.
Item* Item::generateItem(std::string name) {
	if (name == "Potion") {
		return new Potion();
	}
	else if (name == "Mega Potion") {
		return new MegaPotion();
	}
	else if (name == "Grenade"){
		return new Grenade();
	}
	// An invalid item was requested.
	std::cout << "That item does not exist!\n";
	return nullptr;
}

Item* Item::generateRandomItem() {
	int choice = rand() % 100;

	if (choice < 50) {
		return new Potion();
	}
	else if (choice < 75) {
		return new MegaPotion();
	}
	else if (choice < 100){
		return new Grenade();
	}

	// Make sure the # being modded is the count of items.
	std::cout << "Error in modulo for generateRandomItem()!\n";
	return nullptr;
}
```
`````
````` {tab-item} Item.hpp
``` {code-block} cpp
#pragma once
#include "../entities/Entity.hpp"

class Item
{
private:
	std::string name;

protected:
	int power;

public:
	Item(std::string name, int power);
	std::string getName();
	static Item* generateItem(std::string name);
	static Item* generateRandomItem();
	virtual void activate(Entity* target) = 0;
};
```
`````
``````

### MegaPotion

`````` {tab-set}
````` {tab-item} MegaPotion.cpp
``` {code-block} cpp
#include "MegaPotion.hpp"

MegaPotion::MegaPotion() : Item("Mega Potion", 50) {
}

void MegaPotion::activate(Entity* target) {
	target->heal(this->power);
}
```
`````
````` {tab-item} MegaPotion.hpp
``` {code-block} cpp
#pragma once

#include "Item.hpp"

class MegaPotion : public Item
{
public:
	MegaPotion();
	void activate(Entity* target);
private:
	//Note: This will not work prior to C++11!
	//This assignment would need to be done in the constructor.
	//int amount;
};


```
`````
``````

### Potion

`````` {tab-set}
````` {tab-item} Potion.cpp
``` {code-block} cpp
#include "Potion.hpp"

Potion::Potion() : Item("Potion", 20) {
}

void Potion::activate(Entity* target) {
	target->heal(this->power);
}
```
`````
````` {tab-item} Potion.hpp
``` {code-block} cpp
#pragma once

#include "Item.hpp"

class Potion : public Item
{
private:
	// Note: This will not work prior to C++11!
	// This assignment would need to be done in the constructor.
	//int amount = 10;

public:
	Potion();
	void activate(Entity* target);
};


```
`````
``````
