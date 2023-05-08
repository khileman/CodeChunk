Code Chunk
================

## Notes on code

I created this code to use when sectioning off data. The code takes the
top 5 and bottom 5 ranking data points, color codes them and then labels
them. It is useful when looking at data with data points that occur in
similar places and you want to know which points lie at the poles.

“Label” in the initial line of code directs R on which variable should
be used as the label and then you can see the colors used here for the
different sections.

``` r
p <- ggplot(data = df, aes(x = Rank, y = Haven.Score, label = ISO.2)) +
  geom_point(color = case_when(
             df$Rank >= 65 ~ 'dodgerblue',
             df$Rank <= 5 ~ 'forestgreen',
             TRUE ~ 'slateblue1'), 
               size = 3, alpha = 0.8) +
  geom_text_repel(data          = subset(df, Rank >= 65),
                  nudge_y       = 32 - subset(df, Rank >= 65)$Rank,
                  size          = 4,
                  box.padding   = 1.5,
                  point.padding = 0.5,
                  force         = 100,
                  segment.size  = 0.2,
                  segment.color = "grey50",
                  direction     = "x") +
  geom_text_repel(data          = subset(df, Rank <= 5),
                  nudge_y       = 32 - subset(df, Rank <= 5)$Rank,
                  size          = 4,
                  box.padding   = 1.5,
                  point.padding = 0.5,
                  force         = 100,
                  segment.size  = 0.2,
                  segment.color = "grey50",
                  direction     = "x")
```
