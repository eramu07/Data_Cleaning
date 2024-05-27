---
Title: "Data Cleaning with Pandas: A Comprehensive Guide"
Subtitle: "Learn how to clean and preprocess data using Pandas in Python. Discover essential techniques and functions for handling missing values, duplicates, outliers, and more. "
Tags: ["Python","Pandas"]

---

Data cleaning involves removing errors and inconsistencies from a dataset. In data science or machine learning and data analysis , this means ensuring there are no missing values, typos, type mismatches, duplicate rows, **`None`** or **`NaN`** entries, **`empty`** values, unnecessary columns, and more. The Pandas library provides powerful tools for data cleaning, with various functions to address and correct these issues.
In the example below, we'll demonstrate how to clean a mock customer dataset step by step using the **Pandas** library.



## What is Data Cleaning?

Data cleaning is the process of removing errors or inconsistencies from a dataset. To clean a dataset of information in data science or machine learning we have to make sure that there are no missing values, typing errors, type inconsistencies, duplicate rows, `None`, `NaN` or `empty` values, unnecessary columns, and many things more. The **Pandas library** offers us a powerful toolkit for data cleaning. It contains a variety of functions that help us deal with these errors and fix them. 

In the following example, you will see how to clean a mock dataset of information step by step with the **pandas** library. This dataset is a simulation of a customer list.

## Data cleaning tutorial step by step

Step 1: Import Pandas
To start, we need to import the Pandas library in Python.

```py
import pandas as pd
```

After that, use the following code to create the user's data set:

```py

data = pd.DataFrame({
    "user_id": [101, 102, 103, 104, 104, 105, 106, 107, 108, 109, 109],
    "Name": ["Alice", "Bob--", "..Charlie", "David", "David", "Eva/", "Frank9", "Grace", "Helen_", "Ivy", "Ivy"],
    "Last_name": ["Taylor", "Anderson", "Miller", "Martinez", "Martinez", "None", "Garcia", "Rodriguez", "Hernandez", "Lopez", "Lopez"],
    "age": [30, 25, 40, 35, 35, 29, 45, 38, 33, 21, 21],
    "Phone": ["123/456/7890", "234-567-8901", "345_678_9012", "456-789-0123", "456-789-0123", None, "567/890/1234", "678/901_2345", "(789) 012-3456", "890-123-4567", "890-123-4567"],
    "Email": ["alice@example.com", "bob@example.net", "charlie@example.com", "david@example.org", "david@example.org", "eva@example.net", "frank@example.org", "grace@example.com", "helen@example.net", "ivy@example.org", "ivy@example.org"],
    "Not_Useful_column": [None, None, None, None, None, None, None, None, None, None, None]
})

print(data)

```
> The user's data set will display in this way
```bash
   user_id      Name  Last_name  age         Phone               Email      Not_Useful_column  
0      101     Alice     Taylor   30   123/456/7890     alice@example.com          None  
1      102      Bob--  Anderson   25   234-567-8901       bob@example.net          None
2      103  ..Charlie     Miller   40  345_678_9012   charlie@example.com          None
3      104     David  Martinez   35   456-789-0123      david@example.org          None
4      104     David  Martinez   35   456-789-0123      david@example.org          None
5      105      Eva/       None   29          None        eva@example.net          None
6      106    Frank9     Garcia   45  567/890/1234      frank@example.org          None
7      107     Grace  Rodriguez   38  678/901_2345      grace@example.com          None
8      108    Helen_  Hernandez   33  (789) 012-3456    helen@example.net          None
9      109       Ivy      Lopez   21  890-123-4567        ivy@example.org          None
10     109       Ivy      Lopez   21  890-123-4567        ivy@example.org          None

```

Here we use the pandas `DataFrame()` function to create a mock dataset, this dataset contains 7 columns and 11 rows, the columns are, a `user_id` which is the user's unique id, a `Name` column, a `Last_name` column, the user's `age`, the user's `Phone` number, the user's `Email`, and finally a non-useful column called `Not_Useful_column` which we will use as an example of how to delete an unnecessary column from a dataset.

As you can see in the example dataset, the data has some inconsistencies in the columns, a few unnecessary symbols in the `Name` column, and each of the values in the `Phone` column have different syntax which makes it difficult to work with them.

### 1. Delete duplicated rows

The first thing to do when cleaning a dataset is to check and delete duplicated rows. As you can see in the dataset example the rows in index `3` and `4` as well as in index `9` and `10` have the same values, to delete these duplicated rows use the following code:

```py
data = data.drop_duplicates()
```
> data
```bash
  user_id      Name  Last_name  age         Phone               Email      Not_Useful_column  
0      101     Alice     Taylor   30   123/456/7890     alice@example.com          None  
1      102      Bob--  Anderson   25   234-567-8901       bob@example.net          None
2      103  ..Charlie     Miller   40  345_678_9012   charlie@example.com          None
3      104     David  Martinez   35   456-789-0123      david@example.org          None
5      105      Eva/       None   29          None        eva@example.net          None
6      106    Frank9     Garcia   45  567/890/1234      frank@example.org          None
7      107     Grace  Rodriguez   38  678/901_2345      grace@example.com          None
8      108    Helen_  Hernandez   33  (789) 012-3456    helen@example.net          None
9      109       Ivy      Lopez   21  890-123-4567        ivy@example.org          None
```

As you can see the function **`drop_duplicates`** removes all the duplicated rows, in our example dataset, the function successfully removed the rows at index `4` and `10`.

### 2. Delete unnecessary columns

After deleting the duplicated rows, we have to delete all the columns that we're not gonna need, in our case the `Not_Useful_column` column. To delete this column use the following code: 

```py
data = data.drop(columns="Not_Useful_column")
```
> data
```bash
user_id      Name  Last_name  age         Phone             Email  
0      101     Alice     Taylor   30  123/456/7890     alice@example.com   
1      102      Bob--  Anderson   25  234-567-8901       bob@example.net   
2      103  ..Charlie     Miller   40  345_678_9012  charlie@example.com   
3      104     David  Martinez   35  456-789-0123      david@example.org   
5      105      Eva/       None   29          None       eva@example.net   
6      106    Frank9     Garcia   45  567/890/1234     frank@example.org   
7      107     Grace  Rodriguez   38  678/901_2345     grace@example.com   
8      108    Helen_  Hernandez   33  (789) 012-3456   helen@example.net   
9      109       Ivy      Lopez   21  890-123-4567       ivy@example.org 
```

The **`drop`** method with the `columns="Not_Useful_column"` parameter removes the `Not_Useful_column` column from our example dataset, but it must be assigned back to the `df_users` variable to replace its values with those of the new dataset.

### 3. Correct syntax errors in columns

Now that we have removed all the duplicated rows and unnecessary columns, we have to check column by column to see if any of them need to be corrected. Some of the values in the `Name` column have unnecessary symbols at the beginning or end of the name, we can correct these errors with the following code: 

```py
data["Name"] = data["Name"].str.strip("[-_./0-9]{1}")

```
> data
```bash
   user_id     Name  Last_name  age         Phone          Email  
0      101    Alice     Taylor   30  123/456/7890    alice@example.com   
1      102      Bob   Anderson   25  234-567-8901      bob@example.net   
2      103  Charlie     Miller   40  345_678_9012  charlie@example.com   
3      104    David  Martinez   35  456-789-0123     david@example.org   
5      105      Eva       None   29          None      eva@example.net   
6      106    Frank     Garcia   45  567/890/1234    frank@example.org   
7      107    Grace  Rodriguez   38  678/901_2345    grace@example.com   
8      108    Helen  Hernandez   33  (789) 012-3456  helen@example.net   
9      109      Ivy      Lopez   21  890-123-4567      ivy@example.org   

```

The `strip()` method removes empty values at the beginning and at the end of a string, if we pass a specific value as a parameter it will look for that value at the beginning or at the end and remove it. In this example, we call the `strip()` method in the `Name` column `data["Name"].str.strip()` and pass it as parameters the values that we want to remove in a string `[-_./0-9]{1}`, then we access the dataset of the `Name` column `data["Name"]` and we assign it the new values.

### 4. Set a unique pattern for a column

After cleaning the `Name` column , we have to set a single pattern for the `Phone` column, as shown in the example dataset there are different patterns in the values of this column and we have to set a single one for all of them. To do this use the code: 

```py
data["Phone"] = data["Phone"].str.replace(r"[^0-9]", '', regex=True)

data["Phone"] = data["Phone"].apply(
    lambda item: f"{item[0:3]}-{item[3:6]}-{item[6:]}" if type(item) == str and len(item) == 10 else None
)
```
> df_users
```bash
  user_id     Name  Last_name  age       Phone              Email  
0      101    Alice     Taylor   30  123-456-7890     alice@example.com   
1      102      Bob   Anderson   25  234-567-8901       bob@example.net   
2      103  Charlie     Miller   40  345-678-9012   charlie@example.com   
3      104    David   Martinez   35  456-789-0123     david@example.org   
5      105      Eva       None   29         None        eva@example.net   
6      106    Frank     Garcia   45  567-890-1234     frank@example.org   
7      107    Grace  Rodriguez   38  678-901-2345     grace@example.com   
8      108    Helen  Hernandez   33  789-012-3456     helen@example.net   
9      109      Ivy      Lopez   21  890-123-4567       ivy@example.org 
```

Here we want to establish the pattern `000-000-0000` on all the values in the `Phone` column, for this first, we have to delete all the values that are not a number with the **`replace`** function and the syntax `r"[^0-9]",  '', regex=True`, after this, we want to set this pattern on all the phone numbers in this column, for this, we use a `lambda` function and the f-string (format string) expression `f"{item[0:3]}-{item[3:6]}-{item[6:]}"` which is used to embed expressions inside string literals, but we do this only if the current value has a `string` type and have ten characters, as you can see in the index `5` of the `Phone` column we have a `None` value and in the index index `7` of the same column we have a number with only 9 digits, none of these characters meet the condition so they are replaced by a `None` value that will be removed later.

### 5. Delete rows with None values

Now that we have cleaned all the rows in the dataset, we have to delete the rows that contain `None` values and redefine the index of the rows in the dataset.

```py
# Delete columns with None values
data= data.dropna()

# reset the index of the columns
data = data.reset_index(drop=True)
```
> data
```bash
      user_id     Name  Last_name  age       Phone           Email
0      101    Alice     Taylor   30  123-456-7890     alice@example.com
1      102      Bob   Anderson   25  234-567-8901       bob@example.net
2      103  Charlie     Miller   40  345-678-9012   charlie@example.com
3      104    David   Martinez   35  456-789-0123     david@example.org
4      106    Frank     Garcia   45  567-890-1234     frank@example.org
5      107    Grace  Rodriguez   38  678-901-2345     grace@example.com
6      108    Helen  Hernandez   33  789-012-3456     helen@example.net

```

The **`dropna`** function deletes all the rows of a column containing `None` values and the **`reset_index`** function with the `drop=True` parameter reset the index of the rows and delete the old ones.

Now we have a perfectly clean and consistent dataset to start working with. This was a simple example of how to clean the data of a dataset.

## Conclusion

Data cleaning is a very important step before starting to work with a dataset in **data science** or **machine learning**,and **data analysis** it ensures that the data has no syntax errors, `None` or `NaN` values, duplicated rows, unnecessary columns, and many more things. A dataset can be clean in many ways not just the ones seen in this article, Pandas offers a wide variety of functions that helps us with this process. 
