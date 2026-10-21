# User Management 



User Management is only available through CLI.

### Creating a User
There are two separate ways of creating users. The first one relies on your environment, the other one uses a native CakePHP Command.

To create a user through CLI, log in to your environment’s terminal and execute the following command:

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
