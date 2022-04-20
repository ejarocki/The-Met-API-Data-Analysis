**The Metropolitan Museum of Art Collection API
Data Analysis, Modeling, and Forecasting**

By Elijah Jarocki

**Overview**

This is a data science project using The Met's API for analysis, modeling, and forecasting.

**Navigating the Repository**

Final Notebook.ipynb: My final project including code and analysis

LICENSE: License for the dataset

MetObjects.csv: Downloadable csv provided by The Met Open Access API https://github.com/metmuseum/openaccess

README.md: This document, modified from the original fork

Shower at Shōno - Utagawa Hiroshige.jpg: Public Domain photo of a print from The Met's Collection

The-Met-API-Data-Analysis.pdf: Slideshow Presentation of findings

![Shower at Shōno - Utagawa Hiroshige](https://github.com/ejarocki/The-Met-API-Data-Analysis/blob/d8404c0dfdc98d94a4975dc383794cb835fad2b9/Shower%20at%20Sh%C5%8Dno%20-%20Utagawa%20Hiroshige.jpg)

**Business Understanding and Stakeholder**
The Metropolitan Museum of Art has made available to the public an API (application programming interface) that contains almost 500,000 datapoints about their collection. This project uses their downloadable version available at https://github.com/metmuseum/openaccess. This project modifies some aspects of the dataset as detailed below. The data is made available via The Metropolitan Museum of Art's CC0 policy.

In 2019 alone, the Met's net assets increased by $63.1 million. With investments of this magnitude, the Met must ensure that is is growing at a proportional rate with that of the past. Their dataset includes information about both the characteristics of the pieces acquired, and the date when the museum acquired the pieces. I will be using ARIMA to model the time series of their acquisitions and predict and forecast future acquisitions in regard to previous acquisitions.

**Data Understanding and Feature Engineering**

The dataset is made available as a .csv file with 477,804 entries. This data is extremely well-suited for analysis as it is extremely large and dense with information about The Met's own collection. I will primarily focus on the columns:

"AccessionYear" The year in which the museum acquired the piece

"Classification" The type of piece detailed

"Object Begin Date" The time in which the piece was begun

"Object End Date" The time in which the piece was finished

I will engineer an additional column: "Object Time" which is the estimated time it took to create a particular work of art. The dataset has over 400,000 entries, but is still limited as The Met's collection exceeds 2 Million pieces of art work. Similar approaches may easily be used as the dataset grows to include more pieces.

**Initial Data Overview**
Each work of art is listed as a row with 54 columns of attributes.  The attributes "AccessionYear", "Object Begin Date", "Object End Date", and "Classification" all have over 399,000 values. It makes sense to focus on these attributes for our analysis, as they are robust and almost every piece has values for these attributes. I cleaned the "AccessionYear" column to be in uniform format. 

**Modeling**
We will now model The Met's acquisition of paintings. The subset of paintings makes a good choice for our model as the subset is rather small and memory-sensitive while still containing over 8,000 entries. We will create a time series where "AccessionYear" is the index and the total amount of paintings acquired each year is modeled. For our baseline model, I used a naive shift of 1 degree and evaluate the Mean Squared Error for the model. MSE: 98.76867750268372. I then differenced the timeseries and tested for stationarity. My training set was 1870-2000 and my test set was 2000-2022. The ARIMA model i constructed had an AIC on the test set of 1469, and an MSE of 87.0246897054411

**Forecasting** 
I used the ARIMA model to forecast out for the next 10 years. The museum should buy around 84-87 paintings every year from 2023 to 2032. Note that the historical trend of the data is generally large spikes of acquisitions in one year, followed by periods of lower acquisitions. If The Met keeps these numbers as a baseline, they should grow at about the same rate as in the past.

**Conclusions and Recommendations**
The purpose of this project was to identify actionable steps The Met could take in their acquisition process. The museum has a large amount of financial capital, but should grow steadily in accordance to their history to maintain a quality collection. We took the example of the paintings subset of our dataset and constructed an ARIMA model based on historical rates of acquisition. This model performed dramatically better than the baseline model and performed well on the training and test set. The model was able to forecast out stable rates of painting acquisition for the next 10 years into the future. The Met should budget to buy between 84-87 paintings over the next 10 years to maintain a stable rate of growth. This information can greatly assist The Met in their acquisition process and similar models can be built on all classifications of The Met Open Access API Dataset.

**Future Implementations**
Consider the scenario in which The Met was looking for new, contemporary work to feature in an upcoming exhibition. We can use this dataset to filter for works which were created after the year 2000 and took less than two years to complete. The code below accomplishes this task using the "Object End Date" and "Object Time" attributes and lists 40 artists which satisfy this criteria, ordered by number of pieces already in The Met's collection.

The photographer Stephen Shore tops the list. We can now create a subset of the dataset which consists of Stephen Shore's works. Using the Link Resource column, we can easily follow the URL to The Met's website to see images of his work. This process would assist a curator looking for new acquisitions according to certain criteria. I also recommend that further models be built according to different classifications within the dataset to create a cohesive picture of both the history of the museum, and a possible future.

**Below is the original readme from the source**

The Metropolitan Museum of Art Open Access CSV
===================

The [Metropolitan Museum of Art](http://www.metmuseum.org) presents over 5,000 years of art from around the world for everyone to experience and enjoy. The Museum lives in two iconic sites in New York City—The Met Fifth Avenue and The Met Cloisters. Millions of people also take part in The Met experience online.

Since it was founded in 1870, The Met has always aspired to be more than a treasury of rare and beautiful objects. Every day, art comes alive in the Museum's galleries and through its exhibitions and events, revealing both new ideas and unexpected connections across time and across cultures.

The Metropolitan Museum of Art provides select datasets of information on more than 470,000 artworks in its Collection for unrestricted commercial and noncommercial use. To the extent possible under law, The Metropolitan Museum of Art has waived all copyright and related or neighboring rights to this dataset using [Creative Commons Zero](https://creativecommons.org/publicdomain/zero/1.0/). This work is published from: The United States Of America. You can also find the text of the CC Zero deed in the file [LICENSE](https://github.com/metmuseum/openaccess/blob/master/LICENSE) in this repository. These select datasets are now available for use in any media without permission or fee; they also include identifying data for artworks under copyright. The datasets support the search, use, and interaction with the Museum’s collection. 

At this time, the datasets are available in CSV format, encoded in UTF-8. While UTF-8 is the standard for multilingual character encodings, it is not correctly interpreted by Excel on a Mac. Users of Excel on a Mac can convert the UTF-8 to UTF-16 so the file can be imported correctly.

## Additional usage guidelines
### Images not included
Images are not included and are not part of the dataset. Companion artworks listed in the dataset covered by the policy are identified in the [Collection section](http://www.metmuseum.org/art/collection) of the Museum’s website  with the Creative Commons Zero (CC0) icon. 

For more details on how to use images of artworks in The Metropolitan Museum of Art’s collection, please visit our [Open Access](http://www.metmuseum.org/about-the-met/policies-and-documents/image-resources) page.

### Documentation in progress
This data is provided “as is” and you use this data at your own risk. The Metropolitan Museum of Art makes no representations or warranties of any kind. Documentation of the Museum’s collection is an ongoing process and parts of the datasets are incomplete. 

We plan to update the datasets with new and revised information on a regular basis. You are advised to regularly update your copy of the datasets to ensure you are using the best available information.

### Pull requests
Because these datasets are generated from our internal database, we do *not* accept pull requests. If you have identified errors or have extra information to share, please email us at [openaccess@metmuseum.org](mailto:openaccess@metmuseum.org) and we will forward to the appropriate department for review.

### How to clone/download the data file

**Download**: In order to properly download the CSV file and not load the entire file in the browser, visit [this page](https://github.com/metmuseum/openaccess/blob/master/MetObjects.csv) and then right-click on "Download" (if you are using a computer with a trackpad, hold down <kbd>control</kbd> while clicking the link). You should then see a contextual menu where you can choose "Save Link As..."

**Clone**: Note that the CSV file is stored using Git's LFS (large-file storage) system. If you want to clone the repository, you need to run the following command on your console (Terminal on macOS / Git Bash on Windows):

```console
$ git lfs clone https://github.com/metmuseum/openaccess
```

### Attribution
Please consider attributing or citing The Metropolitan Museum of Art's CC0 select datasets, especially with respect to research or publication. Attribution supports efforts to release other datasets in the future. It also reduces the amount of "orphaned data," helping to retain source links.

### Do not misrepresent the dataset
Do not mislead others or misrepresent the datasets or their source. You must not use The Metropolitan Museum of Art’s trademarks or otherwise claim or imply that the Museum or any other third party endorses you or your use of the dataset.

Whenever you transform, translate or otherwise modify the dataset, you must make it clear that the resulting information has been modified. If you enrich or otherwise modify the dataset, consider publishing the derived dataset without reuse restrictions.

The writers of these guidelines thank the [The Museum of Modern Art](http://www.moma.org/), [Tate](http://www.tate.org.uk/), [Cooper-Hewitt](http://www.cooperhewitt.org/), and [Europeana](http://www.europeana.eu/).
