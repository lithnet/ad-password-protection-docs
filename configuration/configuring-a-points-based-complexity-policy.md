# Configuring a points based complexity policy

The password filter policy allows you to require that passwords meet a certain number of points in order to be approved by the filter.

You first select the minimum number of points required for the password to be approved, and then determine how the points are calculated. The following categories can be used to assign points;

* Each character used
* Each number used
* Each lower case letter used
* Each upper case letter used
* Each symbol used
* Use of at least one number
* Use of at least one symbol
* Use of at least one uppercase letter
* Use of at least one lowercase letter

Given the following points allocations, we can see what how many points would be allocated to each password

| Rule                                 | points |
| ------------------------------------ | ------ |
| Each character used                  | 1      |
| Each number used                     | 1      |
| Each lower case letter used          | 2      |
| Each upper case letter used          | 5      |
| Each symbol used                     | 2      |
| Use of at least one number           | 1      |
| Use of at least one symbol           | 5      |
| Use of at least one uppercase letter | 1      |
| Use of at least one lowercase letter | 1      |

### P@ssword1!

| Rule                                 | points |
| ------------------------------------ | ------ |
| Each character used                  | 10     |
| Each number used                     | 1      |
| Each lower case letter used          | 12     |
| Each upper case letter used          | 5      |
| Each symbol used                     | 4      |
| Use of at least one number           | 1      |
| Use of at least one symbol           | 5      |
| Use of at least one uppercase letter | 1      |
| Use of at least one lowercase letter | 1      |
| Total                                | 40     |
