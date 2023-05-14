# AlternateRecommentations
The ML Algorithm to recommend alternate products of a product url.
+ The algorithm first consumes the whole dataset. for example say (150 items for now)
+ Then content-based filtering algorithm is applied to get the cosine-matrix. The cosine matrix is then used for finding which products having the highest similarity in terms of their product information, tags, brans, category


# Help shoppers find product “alternates”

Disclaimer:

- I've created my solution based upon the following e-commerce store API: 'https://www.boysnextdoor-apparel.co/collections/all/products.json?page=1'
- Each page consists of 30 products. So, I've taken the first 5 pages, i.e., 150 items to demonstrate my implementaion.
- The solution has been solely created by myself only.
- It mainly contains two parts. One for implementing ETL, and saving important informations (files) required for testing the solution. Second one, for testing the solution.

Steps to test the solution:

## 1. First Part: Performing ETL and necessary operations

- For example, run the following command with url:

```python
DataPrep('https://www.boysnextdoor-apparel.co').save()
```

It may give the following Output if data already exists in the specified location.

```sh
Please wait while processing in the backend.
Data already exists.

All necessary files is saved for https://www.boysnextdoor-apparel.co.

CONGRATULATIONS! You can proceed with 2nd Step.

```

else, you will see the following output

```sh
Please wait while processing in the backend.
Data doesn't exist, it may take around a minute. Time may vary depends upon the network speed.

Step #1/3
Extracting data from the url: https://www.boysnextdoor-apparel.co/collections/all/products.json?page=1
Extracting data from the url: https://www.boysnextdoor-apparel.co/collections/all/products.json?page=2
Extracting data from the url: https://www.boysnextdoor-apparel.co/collections/all/products.json?page=3
Extracting data from the url: https://www.boysnextdoor-apparel.co/collections/all/products.json?page=4
Extracting data from the url: https://www.boysnextdoor-apparel.co/collections/all/products.json?page=5
Data extraction successful.

Step #2/3
Transforming and Saving extracted data.
data/boysnextdoor-apparel.co.csv saved successfully.

Step #3/3
Calculating and saving import weight file.
weights/boysnextdoor-apparel.co.npy saved successfully.

All necessary files is saved for https://www.boysnextdoor-apparel.co.

CONGRATULATIONS! You can proceed with 2nd Step.
```

## 2. Loading the previously saved data. To perform the API testing

#### 2.1. Load the data

```python
solution = DataLoader()
```

#### 2.2. Test the solution with a product url

```python
name = 'beams-two-pocket-sweater-navy'
item_url = f'https://www.boysnextdoor-apparel.co/products/{name}'

res = solution.FindAlternateGroups(item_url)
print(res)
```

#### Output

```sh
item='beams-two-pocket-sweater-navy'
domain='boysnextdoor-apparel.co'
data reading success
{'product alternates': ['https://www.boysnextdoor-apparel.co/products/beams-two-pocket-sweater-navy', 'https://www.boysnextdoor-apparel.co/products/beams-two-pocket-sweater-white']}
```

#### 2.3. Test the solution with another product url

```python
name = 'ben-davis-heavy-duty-pocket-tee-black'
item_url = f'https://www.boysnextdoor-apparel.co/products/{name}'

res = solution.FindAlternateGroups(item_url)
print(res)
```

#### Output

```sh
item='ben-davis-heavy-duty-pocket-tee-black'
domain='boysnextdoor-apparel.co'
data reading success
{'product alternates': ['https://www.boysnextdoor-apparel.co/products/ben-davis-heavy-duty-pocket-tee-black', 'https://www.boysnextdoor-apparel.co/products/ben-davis-heavy-duty-pocket-tee-white', 'https://www.boysnextdoor-apparel.co/products/ben-davis-pocket-l-s-tee-black', 'https://www.boysnextdoor-apparel.co/products/ben-davis-heavy-duty-pocket-tee-charcoal', 'https://www.boysnextdoor-apparel.co/products/ben-davis-heavy-duty-pocket-tee-ash-grey']}
```

