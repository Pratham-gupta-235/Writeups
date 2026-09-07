# Tryhackme - Pickle Rick

> **Difficulty:** Easy

## Room Info

- Link: [Pickle Rick](https://tryhackme.com/room/picklerick)
- Description: The objective of this room is to find the **three ingredients** hidden throughout the machine.

![1.png](1.png)

---

## 1. Basic **Reconnaissance**

Since the scenario tells us that an HTTP service is available, let's start by visiting the web server.

![2.png](2.png)

The webpage itself doesn't appear to contain anything particularly interesting.

Let's inspect the **page source** to see if the developer left any useful information behind.

![3.png](3.png)

Bingo! Found a Username.
Now that we have a potential username, let's investigate whether the server exposes any other interesting pages or directories.

## 2. Directory Enumeration

![4.png](4.png)

Let's take a look at the website's assets first.

![5.png](5.png)

Nothing particularly useful here. 😒

Let's investigate some other directories.

![6.png](6.png)

**WOW!** We found a login page.

We already have the username. Now we need to find the password.
Instead of guessing, let's continue enumerating the website for information that might reveal it.

## 3. Finding the Password

While exploring the website, we discover another interesting string.

![7.png](7.png)

I don't know what this string represents yet, so let's test whether it could be the password for the login page.

**NICE!** It works.

After logging in, we are presented with something much more interesting:

![8.png](8.png)

a **web shell**.
> NOTE: A web shell allows us to execute commands on the target machine through the browser.

Let's see what files are available using `ls` command. 

![9.png](9.png)

**BINGO!** We found our first ingredient.

## 4. Getting the First Ingredient

Let's try to read the file using the usual `cat` command.

![10.png](10.png)

It looks like `cat` isn't working.

We can try some alternative commands for displaying file contents:

```
head
tail
more
less
```

Fortunately, `less` works.

![11.png](11.png)

And there we have it.

First Ingredient Found! 🥒

## 5. Finding the Second Ingredient

There is another interesting file in the current directory.

![17.png](17.png)

Let's inspect the `/home` directory:

```
ls /home
```

![12.png](12.png)

Oh! there is an account belonging to the `rick` user.

Since the room is called Pickle Rick, this looks promising.

Let's investigate the user's directory.

![13.png](13.png)

**Yup!** We found the second ingredient.

Since `cat` isn't working in this web shell, we'll use `less` again to display the contents.

And there it is:

 Second Ingredient Found! 🥒

## 6. Finding the Third Ingredient

We've found two ingredients. The remaining question is:

**Where is the third ingredient?**

The `root` user's directory seems like a reasonable place to investigate.

However, attempting to access it doesn't give us anything useful.

It looks like our current user doesn't have sufficient privileges.

Let's check what commands our current user is allowed to execute with `sudo`:

```
sudo -l
```

![14.png](14.png)

Interesting.

The output shows that certain commands can be executed with `sudo` **without requiring a password**.

In other words, we have a potential **privilege-escalation path**.

Using the permitted command, we can access the remaining file.

![15.png](15.png)

And there it is:

![16.png](16.png)

 Third Ingredient Found! 🥒
# Congratulations you have just completed the Pickle Rick challenge!
