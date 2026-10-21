#Manual

# Running Commands

Many management commands need to be executed in the EuroKeep container, since they are part of the CakePHP binaries.

The following command, run from your docker directory, opens a shell in the EuroKeep container. Here you can run the setup commands, e.g. create a new user.

```bash
docker compose exec eurokeep /bin/sh
```

# User Manual

This manual is still under construction.

## System Wide Features

There are multiple system wide features activated for EuroKeep.

### Calendar Bar

Many views contain the calendar bar. That part lets you navigate from one month to another which affects the displayed time range.

### Privacy Mode

If you click settings→hide data or show data, you can turn on an off the display of sensitive data. This applies to at least every balance object. No balance, whether an account balance nor transactions of money will then be shown. Also, the IBAN of your accounts will remain hidden until you click show data again.

## User Management

User Management is only available through CLI.

### Creating a User

To create a user, log in to your environment’s CLI and execute the following command:

```bash
/var/www/html # bin/cake user_add
Add a new user.
Please enter email.
> mail@eurokeep.io
Please enter name.
> Mail
Please enter the password.
> Test
User #42, mail@eurokeep.io was created.
That's all, folks.
```

### Resetting Password

To reset an existing user’s password, execute the following command:

```bash
/var/www/html # bin/cake user_reset_password
Select the user of your EuroKeep instance, whose password will be reset.
1: Jan Nox (jan@nox.kiwi)
42: Mail (mail@eurokeep.io)
Please select a user ID (1/11) 
> 42
Please enter the new password.
> Test42!
The password of user #42, mail@eurokeep.io has been changed.
That's all, folks.
```

### Removing a User

Keep in mind, removing a user eradicates its existance. There will be no remains whatsoever, including accounts, transactions.

EVERYTHING will be deleted.

To delete a user from your EuroKeep instance, execute the following command:

```bash
/var/www/html # bin/cake user_delete
Select the user you want to remove from your EuroKeep instance
1: Jan Nox (jan@nox.kiwi)
42: Mail (mail@eurokeep.io)
Please select a user ID (1/11) 
> 42
Please enter the user email address for sake of security.
> mail@eurokeep.io
The user #42, mail@eurokeep.io has been deleted, including all accounts, transactions, etc.
That's all, folks.
```

### 

## Account Management

### Create an Account

To create an account, click the plus icon in your account overview page or directly click here Create an account for your user.

At least, offer a name, an emoji and the account type and the currency the account is working with. Also, add the IBAN. For accounts without IBAN, this field will not be mandatory in the future, but it is for now.

After saving, you can click on the success message and directly go to your new account.

Otherwise, you can go to your account overview and find it there. there.

### Modify an Account

To modify an existing account, select the disired account in your account overview page and then click the pencil icon close to the account overview’s card in the top-right corner.

Then edit anything you want. Don’t forget to click the save icon when done.

### Delete an Account

Deleting an account is possible on the Account’s modification page. Select the disired account in your account overview page and then head to the modification area by clicking the pencil icon in the top-right corner.

On the left bottom area of the form, you can find the trashcan icon. Click that to remove the account.

Keep in mind, that deleting an account will automatically delete all transactions and transfers to that account. There will be no remains of the account whatsoever.

## Booking Money

### Create a Transaction

In your account overview page, select the desired account. Click the plus icon in the top right corner.

Provide the comment, the spent balance and select the category for that transaction.

The category will be selected automatically, if you book a new transfer with the same comment.

During comment input, EuroKeep will try finding a previous booking entry with that commend.

Click the save icon

### Modify a Transaction

In your account’s history, click on an existing transaction to open the transaction modification screen. Change the things you want and dont forget clicking the save icon.

### Delete a Transaction

In your account’s history, click on an existing transaction to open the transaction modification screen. In the bottom left corner you can find the trashcan icon.

### Transfering Money from one Account to Another

Same as Booking Money. But if you select a Transfer Account before adding a new transaction, the negative value of your transfer will also be created for the selected Transfer Account.

However, when editing the transactions, you have to edit both transfers after another. This is not automated.

This behavior also applies to removing a transaction.

## Budgets

Budgets rely on the category management. A budget is a limited amount of money that can be spent for a category and it’s sub-categories.

This feature finds transactions of the current month that match the configured category and it’s sub-categories. These transactions will then be summarized into a value that was spent on the budget.

The transactions can be seen in your Budget Manager if you click a Budget.

The transactions of a budget are only filtered for the categories and the current month, making it possible to analyze a Budget accross multiple accounts which is pretty neat if you want to keep track of your money in terms of where you spend it.

Of course, it does not prevent you from spending money.

### Creating a Budget

Go to your Budget Manager and click the plus icon in the top-right corner.

Enter your title and your limit. Then select a category that should be used. Select the currency and the category your budget will limit.

### Modifying a Budget

Go to your Budget Manager and expand the desired budget by clicking it. Then you can see the pencil icon in the top-right corner of the budget’s card.

Change the fields as you desire, dont’t forget saving your changes afterwards.

### Deleting a Budget

Open the Budget modification form. In the bottom-left corner you can find the trashcan icon that will remove the budget.

Keep in mind: Deleting a Budget will not remove any other data from EuroKeep.

### Visualizing Budgets

Any Budget that you create will appear on the home screen of EuroKeep. This item will only show a progress bar for the budget. The bar represents the available amount. The shorter it gets, the less money is left for that budget.

Clicking on a budget here will bring you right to your Budget Manager and expand the Budget you just clicked. This reveals a more detailed view on that budget - It tells you the limit, the remaining amount or the exceeded amount. Also, it shows all transactions that were found in the current month that were used to build the amound of spent money. From here, you can e.g. edit a transaction directly.

## Monitoring

For now, EuroKeep has a very simple and dumb Prometheus exporter. This is under heavy development and it does not limitate the output whatsoever. Who has access to this controller, will be given all info on all budgets of all users. So handle with absolute caution!

PromQL Exporter

## Summary

For now, there is a simple way to build monthly overviews on your income and spending. You can configure that view to show one or multiple of your accounts. If you open your Summary, it will show you the opening and closing balance of your selected accounts. Also, you will be able to see all spendings and income chronologically. Now you can compare that month to the previous month by using the navigation bar on the page.

Of course, clicking on a transaction or an account leads you to their corresponding edit pages to fix small things ther
