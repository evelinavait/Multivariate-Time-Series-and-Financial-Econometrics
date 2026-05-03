## Stock market volatility analysis using MGARCH model
This is a project for a *Multivariate-Time-Series-and-Financial-Econometrics* course, analysing the volatility dynamics and time-varying correlations between the stock and energy markets using a Multivariate GARCH (MGARCH) model. The analysis employs daily financial data obtained from Yahoo Finance through the `quantmod` package in `R`.

Two representative market indices are used:

- the ^GSPC as a proxy for the United States stock market, and
- the BZ=F as a proxy for the global energy market.

The files `Time-Series-Project.html` and `Time-Series-Project.Rmd` contain the solution to the task in `.html` and `.Rmd` formats. Folder `logo` and `style.css` file were used to style `R Markdown`.

## Data
To download the data, run the code below:
```r
getData <- function(){
  
  library(quantmod)
  
  symbols_assets <- c("^GSPC", "CL=F")
  
  for(sym in symbols_assets){
    
    x <- getSymbols(sym,
                    auto.assign = FALSE,
                    src = "yahoo",
                    from = "2016-01-01",
                    to   = "2026-04-01")
    
    clean_name <- gsub("\\^|=F", "", sym)
    
    assign(clean_name,
           na.omit(x),
           envir = .GlobalEnv)
  }
}
getData()
```

*Consider that:*

- Time is consistent (i.e., ignore non-working days and periods with empty (`NA`) values),
- ignore exchange rate effects,
- $P_t^{(F)}$ - the closing price of the company's shares at time t

Using the closing prices of the company's shares and stock index symbols, calculate the simple returns. Express the simple returns in logarithmic terms and further analyse the logarithmic returns.

Divide the time series into training (80%) and testing (20%) samples. Build the models for the training sample and predict for the testing sample.
