# README


## Data

The data was collected from the St. Lawrence University Women’s Rowing
Team during their 2026 winter training period.

The women’s rowing team ergs five times a week and records data on each
piece that they complete including interval pieces and longer steady
state pieces that build fitness and test pieces that show where their
performance is at. This data includes 7x500m intervals, 5x1000m
intervals, 2k test pieces, and 10k test pieces.

| Variable | Description |
|----|----|
| `ID` | Number indicating athlete |
| `Average` | Average time per 500m for each interval. |
| `IntervalX` | Average time for 500m for that interval. |
| `Rate` | Average strokes per minute during the piece (not included in 1000s). |
| `ClassYear` | What year the athlete is (Freshman, Sophomore, Junior, Senior) |
| `Interval` | Which interval (of 7 or 5) the time is for. |
| `Time` | Time (in seconds) for that interval. |
| `Trial` | Number indicating which number trial the piece is (first of the season, second, third). |
| `Mean` | Average time of all athletes per 500m for that interval and trial. |

## Questions of Interest

1.  How do athletes fare during many short interval pieces compared to
    fewer, longer intervals?

    -\> is there a similar trend between 7x500 and 5x1000?

    -\> what could be the explanation for these trends?

2.  What variables best predict 2k time?

    -\> and what does that prediction look like?

## Graphs

#### 7x500m Intervals

``` r
ggplot(data = x500_long, aes(x = Interval, y = Time)) +
  geom_point(aes(group = Trial, colour = factor(Trial))) +
  geom_line(data = x500_line, aes(x = Interval, y = Mean, 
                                   group = Trial, colour = factor(Trial)), linewidth = 1.5) +
  scale_colour_manual(values = c("purple", "steelblue", "darkorange"), name = "Average of Trial:") +
  labs(y = "Seconds per 500 meters", colour = "AverageTrial", title = "7x500 meter Intervals",
       caption = "Data collected from St. Lawrence University Crew Team Winter 2026")+
  theme_minimal(base_size = 14)
```

![](README_files/figure-commonmark/unnamed-chunk-2-1.png)

#### 5x1000m Intervals

``` r
ggplot(data = x1000_long, aes(x = Interval, y = Time)) +
  geom_point(aes(group = Trial, colour = factor(Trial))) +
  geom_line(data = x1000_line, aes(x = Interval, y = Mean, 
                                   group = Trial, colour = factor(Trial)),linewidth = 1.5) +
  scale_colour_manual(values = c("purple", "darkorange"), name = "Average of Trial:") +
  labs(y = "Seconds per 500 meters", colour = "AverageTrial", title = "5x1000 meter Intervals",
       caption = "Data collected from St. Lawrence University Crew Team Winter 2026")+
  theme_minimal(base_size = 14)
```

![](README_files/figure-commonmark/unnamed-chunk-3-1.png)

#### Linear Regression Visualization

``` r
ggplot(data = pred_10k_2k, aes(x = second10k, y = k2)) +
  geom_point(aes(colour = factor(v1)), alpha = 0.8) +
  geom_line(data = pred_time, aes(x = second10k, y = predicted, 
                                  group = interaction(v1), 
                                  colour = factor(v1)), linewidth = 1) +
  geom_ribbon(data = pred_time, aes(x = second10k, y = predicted,
      ymin = conf.low, ymax = conf.high, group = interaction(v1),
      fill = factor(v1)), alpha = 0.2) +
  labs(colour = "Varsity Boat", fill = "Varsity Boat", y = "2k time (in seconds)",
       caption = "Data collected from St. Lawrence University Crew Team Winter 2026",
       x = "10k time (in seconds)", title = "Predicting 2k time based on 10k time and Varsity Boat Status") +
  scale_colour_manual(values = c("steelblue", "darkorange")) +
  scale_fill_manual(values = c("steelblue", "darkorange")) +
  theme_minimal(base_size = 14)
```

![](README_files/figure-commonmark/unnamed-chunk-5-1.png)
