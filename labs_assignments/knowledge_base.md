### Data Understanding

#### Data Collection

The dataset were initially collected by a [Kaggle enthusiast](https://www.kaggle.com/joebeachcapital) to analyze the way how Airbnb is used to compete with the residential housing market.

The dataset were scraped from the Airbnb website and published on [Kaggle platform](https://www.kaggle.com/datasets/joebeachcapital/airbnb), from which it was downloaded by our team.

No problems were encountered during data collection phase.

#### Data Description

The data were acquired in tabular format as ".csv" file. It is also possible to acquire the data in ".geojson" format.

The basic "surface" features of the dataset are:
- The quantity of the data: `494 954` unique datapoints;
- The amount of features: `89` including one target variable;
- Feature data types distribution:
  * Object/Categorical: `55`;
  * Float: `33`;
  * Int: `1` - ID column.
- The dataset has `7793336` missing values (`~17.7%` of all values);
- Top 10 features with missing values:
  * Has Availability -               `485647` (`~98.0%`) (Object/Categorical)
  * Square Feet -                    `482745` (`~97.5%`) (Float)
  * License -                        `480358` (`~97.0%`) (Object/Categorical)
  * Host Acceptance Rate -           `452696` (`~91.5%`) (Object/Categorical)
  * Monthly Price -                  `398863` (`~80.6%`) (Float)
  * Weekly Price -                   `397207` (`~80.3%`) (Float)
  * Neighbourhood Group Cleansed -   `392791` (`~79.4%`) (Object/Categorical)
  * Jurisdiction Names -             `360401` (`~72.8%`) (Object/Categorical)
  * Notes -                          `297364` (`~60.0%`) (Object/Categorical)
  * Security Deposit -               `290942` (`~58.8%`) (Float)

I decided to drop all variables with the amount of missing values >= `15%`.

Overall, the data quality satisfies the requirements and it is assumed that the data loss should not be substantial.

#### Data Exploration

Our initial target variable - "Review Scores Value". However, as we can see, almost `26%` of this values are missing. So, from my point of view we can predict the review scores using relevant features. I do not think that using simple imputing techniques would suit us here since most of NaNs mean that no scores were given to a particular place.

From business perspective, predicting the daily price might be more relevant by helping landlords set the price in appropriate range. For your information, the percentage of missing Reviews vs Price is `0.26` / `0.01`.

So, from that very moment, I decided to change my business objective as well as target variable - daily price ("Price"). By accurately predicting the price we will make the lifes of both customers and landlords easier. This will guarantee the price adequacy of particular property. So, neither the customers or landlords will be fooled by incorrect price.

#### Types of data
The provided dataset will be splitted in 3 sets of data based on its type:
- `Categorical`: Contains categorical data with the amount of unique values <= `50` (e.g. "Property Type", "Bed Type", etc.);
- `Object`: Contains non-numerical data with the amount of unique values > `50` (e.g. "Summary", "Description", etc.);
- `Numerical`: Contains numerical data.

As a result, we have the following datasets:
- `Categorical`:
    * Room Type;
    * Experiences Offered;
    * Bed Type;
    * Cancellation Policy;
    * Country;
    * Property Type.
- `Object`:
    * ID;
    * Listing Url;
    * Scrape ID;
    * Last Scraped;
    * Name;
    * Summary;
    * Description;
    * Picture Url;
    * Host URL;
    * Host Name;
    * Host Since;
    * Host Location;
    * Host Thumbnail Url;
    * Host Picture Url;
    * Host Verifications;
    * Street;
    * Neighbourhood Cleansed;
    * City;
    * State;
    * Zipcode;
    * Market;
    * Smart Location;
    * Country Code;
    * Amenities;
    * Calendar Updated
    * Calendar last Scraped;
    * Geolocation;
    * Features.
- `Numerical`:
    * Host Listings Count;
    * Host Total Listings Count;
    * Accommodates;
    * Bathrooms;
    * Bedrooms;
    * Beds;
    * Price;
    * Guests Included;
    * Extra People;
    * Minimum Nights;
    * Maximum Nights;
    * Availability 30;
    * Availability 60;
    * Availability 90;
    * Availability 365;
    * Number of Reviews;
    * Calculated host listings count.

`TODO`:
- Set a threshold for missing values - `Done`;
- Drop the features with missing values >= threshold - `Done`;
- Set a threshold for categorical variables - `Done`;
- Select the subset of object variables with unique vals amount <= threshold - `Done`;
- Plot distribution for numerical and categorical variables - `Done`;
- Find out additional EDA techniques - `Done`. Note: your imagination;
- Plot a relationships between cat features and price;
- Remove all rows with the amount of missing features >= threshold;
- Find a way to fill the missing values;
- Find a way to encode the cat variables;
- Perform dimensionality reduction (Or try different models) to select the most relevant variables;
- Perform EDA on selected subset of variables;
- Summarize the results in the report.

#### Numerical and Categorical distributions

For categorical data we have the following distribution:
<Image>

For numerical data we have the following distribution:
<Image>

#### Outliers

In the numerical dataset we have the following amount of outliers:
- Bathrooms: 114272;
- Calculated host listings count: 89056;
- Host Listings Count: 63362;
- Host Total Listings Count: 63362;
- Beds: 57328;
- Number of Reviews: 55580;
- Price: 48906;
- Guests Included: 40629;
- Minimum Nights: 38496;
- Extra People: 34474;
- Accommodates: 24433;
- Bedrooms: 18020;
- Maximum Nights: 703;
- Availability 30: 0;
- Availability 60: 0;
- Availability 90: 0;
- Availability 365: 0.

Boxplots:
<Image>

#### Data Quality

The following transformations can be made on categorical variables:
- Room type can be combined into 2 or 3 categories;
- Experiences offered can be dropped due to appearance of a single value in 99% of the cases;
- Small amount of countries can be combined into a single group;
- Most property types can be combined into a single group.

Additionally, latitude and longitude can be used to calculate the distance between city center and each property in our dataset. I assume that there might be a significant correlation between price and distance from the city center to property.