[![Build
Status](https://travis-ci.org/ropensci/rfishbase.svg?branch=rfishbase2.0)](https://travis-ci.org/ropensci/rfishbase)
[![Coverage
Status](https://coveralls.io/repos/ropensci/rfishbase/badge.svg?branch=rfishbase2.0)](https://coveralls.io/r/ropensci/rfishbase?branch=rfishbase2.0)

Welcome to `rfishbase 2.0`.

This branch represents a work in progress and will not be functional
until the FishBase API is released. At this time endpoints are still
being added to the API and implemented in the package.

Quickstart
----------

Install:

      devtools::install_github("ropensci/rfishbase@rfishbase2.0")

Assemble a list of species:

    library(rfishbase)
    my_species <- c(common_to_sci("trout"), 
                    species_list(Genus = "Labriodes"))

Extract data tables for the listed species:

    species_info(my_species)

    ## Warning in check_and_parse(resp): client error: (404) Not Found

    ## Warning in error_checks(parsed, resp = resp): route not found for query
    ## http://fishbaseapi.info/species?SpecCode=integer%280%29&limit=100&fields=

    ## Source: local data frame [8 x 97]
    ## 
    ##   SpecCode        Genus      Species SpeciesRefNo           Author
    ## 1      238        Salmo       trutta         4779   Linnaeus, 1758
    ## 2      239 Oncorhynchus       mykiss         4706  (Walbaum, 1792)
    ## 3      246   Salvelinus   fontinalis         5723 (Mitchill, 1814)
    ## 4     1858    Lethrinus     miniatus         2295  (Forster, 1801)
    ## 5     2691   Salvelinus        malma         5723  (Walbaum, 1792)
    ## 6     4826 Plectropomus    leopardus         5222 (Lacepède, 1802)
    ## 7     8705 Schizothorax richardsonii         4832     (Gray, 1832)
    ## 8    14606      Arripis    truttacea         9701   (Cuvier, 1829)
    ## Variables not shown: FBname (chr), PicPreferredName (chr),
    ##   PicPreferredNameM (chr), PicPreferredNameF (chr), PicPreferredNameJ
    ##   (chr), FamCode (int), Subfamily (chr), GenCode (int), SubGenCode (int),
    ##   BodyShapeI (chr), Source (chr), Remark (chr), TaxIssue (chr), Fresh
    ##   (lgl), Brack (lgl), Saltwater (lgl), DemersPelag (chr), AnaCat (chr),
    ##   MigratRef (chr), DepthRangeShallow (dbl), DepthRangeDeep (dbl),
    ##   DepthRangeRef (int), DepthRangeComShallow (dbl), DepthRangeComDeep
    ##   (dbl), DepthComRef (int), LongevityWild (dbl), LongevityWildRef (int),
    ##   LongevityCaptive (dbl), LongevityCapRef (int), Vulnerability (dbl),
    ##   Length (dbl), LTypeMaxM (chr), LengthFemale (dbl), LTypeMaxF (chr),
    ##   MaxLengthRef (int), CommonLength (chr), LTypeComM (chr), CommonLengthF
    ##   (chr), LTypeComF (chr), CommonLengthRef (int), Weight (dbl),
    ##   WeightFemale (chr), MaxWeightRef (int), Pic (chr), PictureFemale (chr),
    ##   LarvaPic (chr), EggPic (chr), ImportanceRef (chr), Importance (chr),
    ##   PriceCateg (chr), PriceReliability (chr), Remarks7 (chr),
    ##   LandingStatistics (chr), Landings (chr), MainCatchingMethod (chr), II
    ##   (chr), MSeines (lgl), MGillnets (lgl), MCastnets (lgl), MTraps (lgl),
    ##   MSpears (lgl), MTrawls (lgl), MDredges (lgl), MLiftnets (lgl),
    ##   MHooksLines (lgl), MOther (lgl), UsedforAquaculture (chr), LifeCycle
    ##   (chr), AquacultureRef (chr), UsedasBait (chr), BaitRef (chr), Aquarium
    ##   (chr), AquariumFishII (chr), AquariumRef (chr), GameFish (lgl), GameRef
    ##   (int), Dangerous (chr), DangerousRef (int), Electrogenic (chr),
    ##   ElectroRef (int), Complete (chr), GoogleImage (lgl), Comments (chr),
    ##   Profile (chr), PD50 (chr), Entered (int), DateEntered (date), Modified
    ##   (int), DateModified (date), Expert (int), DateChecked (date), TS (chr)

Package Overview
----------------

Design principles:

Most functions are designed to take a character vector of species names
as input and return a `data.frame` as output; usually with species as
rows and columns as variables measured on the species.

Species names must be valid scientific names as recognized by FishBase.

Getting good species names:

-   `species_list()` Is probably the most common entry point for
    generating a list of species by specifying a higher taxonomic group
    of interest.  
-   `common_to_sci()` Gives a list of scientific names matching the
    queried common name(s).
-   `synonyms()` Scientific names change frequently and thus taxonomy
    differs across databases. Consequently, FishBase may not use the
    same scientific name you are familiar with. This function will
    return a table of species names that FishBase recognizes as synonyms
    of the query, with a column, `Valid` indicating if it is the
    accepted species name used in the FishBase database or not. For any
    of the other queries to work that rely on scientific names, be sure
    to use this accepted synonym.
