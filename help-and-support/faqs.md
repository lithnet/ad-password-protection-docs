# Frequently asked questions

## Can I apply the password filtering to only a specified group of users?
Unfortunately not. The password filter applies to all users in the domain. A future version of Lithnet Password Protection is planned which will implement fine-grained password policies.

## Can users be shown a more informative message about why their password was rejected?
Windows does not provide a native mechanism to report the reason why a password change was rejected. 

## I've added a banned word, but passwords containing that word are still being accepted. Why?
The banned word feature isn't designed to block strings of text. It's an intelligent filter designed to prevent users creating passwords based on simple words and common substitutions. It will prevent the creation of passwords that are susceptible to offline brute force attacks and password guessing techniques, while allowing users to create longer, more complex passwords and passphrases that may include those words.

The password goes through a normalization process that removes common substitutions (e.g. "@" to "a", "1" to "i", etc) and then checks for the presence of the banned word. If the banned word is part of a longer password that has not been altered with common substitutions, it will not be blocked. For example, if "blue" is a banned word, "blue123" will be blocked, but "myfavoritecolorisblue" will not be blocked.

If you need to block a string of text outright, use the regex policy to block that specific sequence of characters.

You can read up on the specifics of how our [normalization algorithm works](/advanced-help/normalization-rules.md).
