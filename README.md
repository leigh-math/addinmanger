# RStudio addins manager
[![Build Status](https://travis-ci.org/csgillespie/addinmanger.svg?branch=master)](https://travis-ci.org/csgillespie/addinmanger)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/addinmanger)](https://cran.r-project.org/package=addinmanger)

RStudio addins let you execute a bit of R code or a Shiny app through the RStudio IDE,
either via the Addins dropdown menu or with a keyboard shortcut. 
This package is an RStudio addin for managing **other** addins. To run these addins, you need the
latest version of [RStudio](https://www.rstudio.com/). 

## Installation

The package can be installed via `devtools`

```
## Need the latest version of DT as well
devtools::install_github('rstudio/DT')
devtools::install_github("csgillespie/addinmanger")
```


## Running addins

After installing the package, the _Addins_ menu toolbar will be populated with the 
new, exported addins. This addin is called __Addin Manager__.

When you lauch the addin, a DT table will be launched:

![alt text](https://raw.github.com/csgillespie/addinmanger/master/images/screenshot.png)

The highlighted addins are that have been already installed.

When you click **Done**

 * Highlighted addins will be installed.
 * Un-highlighted addins will be removed.







## Using the package

To use this package, you will need a [data API](https://www.typeform.com/help/data-api/)
key. With this key in position, you can then list your available forms

```
api = "XXXXX"
typeforms = get_all_typeforms(api)
```

If you don't pass your `api` key as an argument, it will attempt to read the variable
`Sys.getenv("typeform_api")`.

You can download data from a particular typeform via
```
## uid can be obtained from the typeforms data set 
## above
get_results(uid, api)
```

There are a number of options for downloading the data. For example

```
## Only completed forms
get_results(uid, api, completed=TRUE)
## Results since the 1st Jan
get_results(uid, api, since=as.Date("2016-01-01"))
```

See the `?get_results` help page for other options.

## Example: Multiple Filters / Order

Imagine we only want to fetch only the last 10 completed responses.

  * We only want completed results, so we add the parameter `completed=TRUE`.
  * The results need to be ordered by newest results first, so we add the parameter `order_by="date_submit_desc"`
  * We only want 10 results maximum, so we add the parameter `limit=10`
  
This gives the function call

```
get_results(uid, api, completed=TRUE, order_by="date_submit_desc", limit=10)
```

## Other information

 * If you have any suggestions or find bugs, please use the github [issue tracker](https://github.com/csgillespie/typeform/issues).
 * Feel free to submit pull requests.
 * I intend to submit the package to CRAN within the next week or so.
