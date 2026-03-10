# Évaluation — Bank Account Console App

## Description

Ce TP consiste à développer une **simulation simple d’un système bancaire** en utilisant le langage **Kotlin**.

Le programme permet de créer différents types de comptes bancaires et d'effectuer plusieurs opérations comme :

- vérifier le **solde du compte**
- **retirer de l'argent**
- **déposer de l'argent**
- **fermer l'application**

Le programme gère trois types de comptes :

- **Debit account**
- **Credit account**
- **Checking account**

Chaque type de compte possède des règles spécifiques pour les opérations de dépôt et de retrait.

---

# Objectifs du TP

Les objectifs de ce laboratoire sont :

- Comprendre l'utilisation des **conditions (`if`, `when`)**
- Utiliser les **fonctions**
- Manipuler des **variables**
- Simuler un **système bancaire simple**
- Utiliser des **boucles (`while`)**
- Comprendre la gestion de **différents types de comptes**

---

# Structure du projet

```
banking-system/
│
├── banking.kt
└── banking.jar
```

- **banking.kt** : code source Kotlin  
- **banking.jar** : application compilée

---

# Code source du programme

```kotlin
fun main() {
    
    println("Welcome to your banking system.")
    println("What type of account would you like to create?")
    println("1. Debit account")
    println("2. Credit account")
    println("3. Checking account")

    var accountType = ""
    var userChoice = 0

    while (accountType == "") {
        println("Choose an option (1, 2 or 3)")
        userChoice = (1..5).random()
        println("The selected option is ${userChoice}.")

        when (userChoice) {
            1 -> accountType = "debit"
            2 -> accountType = "credit"
            3 -> accountType = "checking"
            else -> continue
        }
    }

    println("You have created a ${accountType} account.")

    
    var accountBalance = (0..1000).random()

    if (accountType == "credit") {
        accountBalance = -(0..1000).random()
        println("Credit account detected: balance is a debt => ${accountBalance} dollars.")
    }

    println("The current balance is ${accountBalance} dollars.")

    val money = (0..1000).random()
    println("The amount you transferred is ${money} dollars.")

    fun withdraw(amount: Int): Int {
        accountBalance -= amount
        println("You successfully withdrew ${amount} dollars. The current balance is ${accountBalance} dollars.")
        return amount
    }

    fun debitWithdraw(amount: Int): Int {
        if (accountBalance == 0) {
            println("Can't withdraw, no money on this account!")
            return accountBalance
        } else if (amount > accountBalance) {
            println("Not enough money on this account! The current balance is ${accountBalance} dollars.")
            return 0
        } else {
            return withdraw(amount)
        }
    }

    fun deposit(amount: Int): Int {
        accountBalance += amount
        println("You successfully deposited ${amount} dollars. The current balance is ${accountBalance} dollars.")
        return amount
    }

    fun creditDeposit(amount: Int): Int {
        if (accountBalance == 0) {
            println("This account is completely paid off! Do not deposit money!")
            return 0
        } else if (accountBalance + amount > 0) {
            println("Deposit failed, you tried to pay off an amount greater than the credit balance. The current balance is ${accountBalance} dollars.")
            return 0
        } else if (amount == -accountBalance) {
            accountBalance = 0
            println("You have paid off this account!")
            return amount
        } else {
            return deposit(amount)
        }
    }

    
    fun transfer(mode: String) {
        val transferAmount: Int

        when (mode) {
            "withdraw" -> {
                transferAmount = if (accountType == "debit") debitWithdraw(money) else withdraw(money)
                println("The amount you withdrew is ${transferAmount} dollars.")
            }
            "deposit" -> {
                transferAmount = if (accountType == "credit") creditDeposit(money) else deposit(money)
                println("The amount you deposited is ${transferAmount} dollars.")
            }
            else -> return
        }
    }

    var isSystemOpen = true
    var option = 0

    while (isSystemOpen) {
        println("What would you like to do?")
        println("1. Check bank account balance")
        println("2. Withdraw money")
        println("3. Deposit money")
        println("4. Close the app")
        println("Which option do you choose? (1, 2, 3 or 4)")

        option = (1..5).random()
        println("The selected option is ${option}.")

        when (option) {
            1 -> println("The current balance is ${accountBalance} dollars.")
            2 -> transfer("withdraw")
            3 -> transfer("deposit")
            4 -> {
                isSystemOpen = false
                println("The system is closed")
            }
            else -> continue
        }
    }
}
```

---

# Fonctionnement du programme

Le programme simule un **système bancaire interactif**.

### Étape 1 : Création du compte

L'utilisateur peut créer :

- un **Debit account**
- un **Credit account**
- un **Checking account**

Le type de compte influence le comportement des opérations.

---

### Étape 2 : Initialisation du solde

Le solde du compte est généré aléatoirement :

```
0 à 1000 dollars
```

Pour un **Credit account**, le solde devient **négatif**, représentant une **dette**.

---

### Étape 3 : Menu principal

Le programme affiche un menu :

```
1. Check bank account balance
2. Withdraw money
3. Deposit money
4. Close the app
```

L'utilisateur peut effectuer différentes opérations.

---

### Étape 4 : Retrait d'argent

Pour un **debit account**, certaines conditions sont vérifiées :

- impossible de retirer si le solde est **0**
- impossible de retirer plus que le **solde disponible**

---

### Étape 5 : Dépôt d'argent

Pour un **credit account**, le dépôt sert à **rembourser la dette**.

Certaines règles s'appliquent :

- impossible de payer plus que la dette
- lorsque la dette devient **0**, le crédit est **remboursé**

---

# Compilation du programme

Pour compiler le programme Kotlin :

```bash
kotlinc banking.kt -include-runtime -d banking.jar
```

---

# Exécution du programme

Pour exécuter l'application :

```bash
java -jar banking.jar
```
<img width="1051" height="655" alt="Capture d’écran du 2026-03-10 23-38-20" src="https://github.com/user-attachments/assets/ceb089eb-fa9c-40eb-93b6-1b5f79d4508f" />

---

# Concepts Kotlin utilisés

Ce TP utilise plusieurs concepts importants :

- **variables**
- **fonctions**
- **conditions (`if`, `when`)**
- **boucles (`while`)**
- **fonctions imbriquées**
- **interpolation de chaînes**
- **génération de nombres aléatoires**

---


# Auteur
Ait Hmad Oussama
