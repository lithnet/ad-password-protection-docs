# Configuring a length based complexity policy

The password filter policy allows you to assign different complexity requirements to passwords based on their length. This allows you to 'reward' length over choice of character sets.

For example you can require 3 out of 4 character sets for passwords under 13 characters in length, but anything over that has no special requirements.

The `Enable length-based complexity rules` policy allows you to define three separate thresholds each with their own requirements.

Each threshold contains 3 settings
* Length - Specify the length of password that the settings apply to.
* Require a number of character sets to be present. Of the character set types available (lower case letter, upper case letter, number and symbol). Specify how many must be present in the password. Setting this to `3` is equivalent to Active Directory's built-in password complexity policy settings.
* Require specific character sets to be present. Use this option to enforce that all the specific character sets you selected are present in the password before approving it.

If you only require two levels of threshold, leave threshold 3 empty. If you only require a single threshold, leave thresholds 2 and 3 empty.

