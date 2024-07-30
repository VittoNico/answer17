
## answer17
```R
library(httr)
library(jsonlite)

base_url <- "https://webservice.wikipathways.org"

search_aop_pathways <- function(search_text = "AOP") {
  response <- GET(
    url = paste0(base_url, "/findPathwaysByText"),
    query = list(query = search_text, format = "json")
  )
  
  if (response$status_code == 200) {
    # Parse the JSON response
    response_content <- content(response, as = "text", encoding = "UTF-8")
    parsed_response <- fromJSON(response_content, flatten = TRUE)
    
    # Extract pathways information
    pathways <- parsed_response$searchResults$pathways
    return(pathways)
  } else {
    stop("Failed to retrieve data from WikiPathways API")
  }
}

aop_pathways <- search_aop_pathways()

if (!is.null(aop_pathways)) {
  print(aop_pathways)
} else {
  print("No pathways found containing the text 'AOP'")
}

```
