### Assignment08

UNI: mg4122


```python
import requests
import os
import json

```

## Accessing the Metropolitan Museum of Art Collection Key

### The function is about the Metropolitan Museum of Art Collection. Using this function, you could get the department name, id as well as the status such as if it is popular, the accessionNumber, accessionYear, etc. given the ObjectID of a collection. Here, we want to focus on the department name and Department ID of the Metropolitan Museum of Art Collection Key

#### At this time, they do not reuire API users to register or obtain an API key to use the service. 
#### Please limited request to 80 requests per second. 
#### The documentation could be found here : https://metmuseum.github.io/

## Object searching endpoints

#### I will use the "departments" for the Metropolitan. Documentation is available at: https://metmuseum.github.io/#departments
#### The endpoint requires the following request format: collection/v1/search?q={filter}




```python
### Get the json format of the response
## No need of the API for Metropolitan API
params={'format':'json'}
r = requests.get('https://collectionapi.metmuseum.org/public/collection/v1/departments',params=params)
```


```python
r.status_code
```




    200




```python
r.text[:100]
```




    '{"departments":[{"departmentId":1,"displayName":"American Decorative Arts"},{"departmentId":3,"displ'




```python
r.headers
```




    {'Access-Control-Allow-Origin': '*', 'Content-Type': 'application/json; charset=UTF-8', 'Vary': 'Origin', 'Date': 'Mon, 11 Jan 2021 03:03:54 GMT', 'Set-Cookie': 'visid_incap_1662004=AZh9t3+iS+qwjIAK18N8axnA+18AAAAAQUIPAAAAAADPce9bU0gJH9veupYG5yT1; expires=Mon, 10 Jan 2022 10:04:09 GMT; HttpOnly; path=/; Domain=.metmuseum.org, incap_ses_8074_1662004=atL6XqTOr2J4mO6FRJwMcBnA+18AAAAAgWYWsDxQC+gadyYAwRbB8g==; path=/; Domain=.metmuseum.org, ___utmvmNpVuKBSmB=TVYZcTAIaqC; path=/; Max-Age=900, ___utmvaNpVuKBSmB=sxm\x01Ytup; path=/; Max-Age=900, ___utmvbNpVuKBSmB=vZE\r\n    XhjOwala: ptA; path=/; Max-Age=900', 'X-CDN': 'Incapsula', 'Content-Encoding': 'gzip', 'Transfer-Encoding': 'chunked', 'X-Iinfo': '14-72074013-72074021 NNYN CT(4 11 0) RT(1610334233526 56) q(0 0 0 -1) r(1 1) U12'}




```python
r.text
```




    '{"departments":[{"departmentId":1,"displayName":"American Decorative Arts"},{"departmentId":3,"displayName":"Ancient Near Eastern Art"},{"departmentId":4,"displayName":"Arms and Armor"},{"departmentId":5,"displayName":"Arts of Africa, Oceania, and the Americas"},{"departmentId":6,"displayName":"Asian Art"},{"departmentId":7,"displayName":"The Cloisters"},{"departmentId":8,"displayName":"The Costume Institute"},{"departmentId":9,"displayName":"Drawings and Prints"},{"departmentId":10,"displayName":"Egyptian Art"},{"departmentId":11,"displayName":"European Paintings"},{"departmentId":12,"displayName":"European Sculpture and Decorative Arts"},{"departmentId":13,"displayName":"Greek and Roman Art"},{"departmentId":14,"displayName":"Islamic Art"},{"departmentId":15,"displayName":"The Robert Lehman Collection"},{"departmentId":16,"displayName":"The Libraries"},{"departmentId":17,"displayName":"Medieval Art"},{"departmentId":18,"displayName":"Musical Instruments"},{"departmentId":19,"displayName":"Photographs"},{"departmentId":21,"displayName":"Modern Art"}]}'




```python
r.encoding
```




    'UTF-8'



## convert the results to the dataframe


```python
x=r.json()
dF = pd.DataFrame.from_dict(x['departments'])
```


```python
dF
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>departmentId</th>
      <th>displayName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>American Decorative Arts</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>Ancient Near Eastern Art</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>Arms and Armor</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>Arts of Africa, Oceania, and the Americas</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>Asian Art</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>The Cloisters</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>The Costume Institute</td>
    </tr>
    <tr>
      <th>7</th>
      <td>9</td>
      <td>Drawings and Prints</td>
    </tr>
    <tr>
      <th>8</th>
      <td>10</td>
      <td>Egyptian Art</td>
    </tr>
    <tr>
      <th>9</th>
      <td>11</td>
      <td>European Paintings</td>
    </tr>
    <tr>
      <th>10</th>
      <td>12</td>
      <td>European Sculpture and Decorative Arts</td>
    </tr>
    <tr>
      <th>11</th>
      <td>13</td>
      <td>Greek and Roman Art</td>
    </tr>
    <tr>
      <th>12</th>
      <td>14</td>
      <td>Islamic Art</td>
    </tr>
    <tr>
      <th>13</th>
      <td>15</td>
      <td>The Robert Lehman Collection</td>
    </tr>
    <tr>
      <th>14</th>
      <td>16</td>
      <td>The Libraries</td>
    </tr>
    <tr>
      <th>15</th>
      <td>17</td>
      <td>Medieval Art</td>
    </tr>
    <tr>
      <th>16</th>
      <td>18</td>
      <td>Musical Instruments</td>
    </tr>
    <tr>
      <th>17</th>
      <td>19</td>
      <td>Photographs</td>
    </tr>
    <tr>
      <th>18</th>
      <td>21</td>
      <td>Modern Art</td>
    </tr>
  </tbody>
</table>
</div>



### API Client Function


```python
#### Use this function to find the department name given the department ID of the metropolitan data 

def get_department_name(departmentId):
    url='https://collectionapi.metmuseum.org/public/collection/v1/departments'
    r=requests.get(url)
    
## Check the status of request function
    if r.status_code != 200:
        print('API request is unsucessful!')
    elif r.status_code == 200:
        print('API request is sucessful!')
        data=r.json()
        global departmentlist
        
        departmentlist=pd.DataFrame.from_dict(data['departments'])
        #print()
        #data = r.json()## convert the results to json format
        #print(json.dumps(data, indent=2, sort_keys=True))
        return departmentlist.loc[departmentlist['departmentId']== departmentId]
```


```python
## Try if the function could work
a = get_department_name(1)
a
```

    API request is sucessful!





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>departmentId</th>
      <th>displayName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>American Decorative Arts</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
