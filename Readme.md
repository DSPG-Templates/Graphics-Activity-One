# Activity Objective

The goal of Graphics Activities are to improve familiarity with
graphical libraries and their customization abilities. For this
activity, the goal is to recreate a box plot generated using the
`ggplot2` package in R.

The plot you will recreate is the following. ![Activity One Box
Plot](imgs/Graphics_Activity_One.jpg)

# Helpful Tips

## Resources

For this activity, the [R Graphics Cookbook](https://r-graphics.org/)
will be extremely helpful. If you are unsure of what any functions do,
running `?function_name` will open the documentation menu in RStudio.
For example, to understand what the `ggplot()` function does, we could
run `?ggplot`.

## Required Packages

Install the following packages if you don’t have them.

    install.packages("dplyr")
    install.packages("ggplot2")
    install.packages("stringr")

Load all libraries

    library(dplyr)
    library(ggplot2)
    library(stringr)

## Data and Additional Variables

This is the data set you will use to make the plots

    # Load the data set from dplyr as storms_df
    storms_df <- dplyr::storms
    storms_df

These are some additional variables/formatting you will need

    # The list of statuses you will want to use
    status_list <- c("tropical depression", "tropical storm", "hurricane", "extratropical")

    # Convert the levels of the Pressure column factor to match those of the status_list
    storms_df$status <- factor(storms_df$status, levels = status_list)

    # This will be required to make an annotation on the graphic
    pressure_quantile <- quantile(storms_df$pressure, probs = c(.25, .75, .5))

## Formatting Notes

The following are notes on the formatting required to make the plot as
identical as possible.

-   The annotated `IQR` red rectangle in the graphic has an `alpha=.1`.
-   The annotated `IQR` text has a `y=2.5` and an
    `x=pressure_quantile[[3]] - 3`
-   The y-axis texts use
    `stringr::str_to_title(levels(storms_df$status))` for text
    formatting
-   The colors of the box plots use the 3rd palette from the
    `scale_fill_brewer()` function
-   Sizes of texts are…
    -   Title is `size=rel(1.5)`
    -   Title of x is `size=rel(1.10)` and margins are
        `margin(t = 5,b = 5)`
    -   Text of y is `size=rel(1.10)`
    -   Text of x is `size=rel(1.10)`
-   caption has a margin of `margin(t = 5)`
-   plot has a margin of `margin(r = 20,l = 5)`

Feel free to ask any questions on any item on the plot if you are unsure
about the exact values.

## Submission

The submission will be the code used to generate the graphic and the
image itself. You can save the graphic using the following code.
Remember to add metadata to the top of your submission file.

    ggsave(filename = "result/Graphics_Activity_One.jpg", plot = plot, width = 10, height = 8, units = "in", dpi = 300)
