Initial Data Cleaning
================

Strategy is to load all scenes in as rasterstacks and the lcz and
polygon information as a dataframe.

The scenes are then stacked and converted to a dataframe.

LCZ and scene data is bound by column and saved in `results` as
`hk_df.rds` file

``` r
lcz <- readRDS(here("results", "lcz_and_poly_ids.RDS"))

# make file lists
scene_1 <- list.files(here("data/hong_kong/landsat_8", "LC81220442013333LGN00"),
                       pattern='.tif', all.files=TRUE, full.names=TRUE)

scene_2 <- list.files(here("data/hong_kong/landsat_8", "LC81220442014288LGN00"),
                       pattern='.tif', all.files=TRUE, full.names=TRUE)

scene_3 <- list.files(here("data/hong_kong/landsat_8", "LC81220442014320LGN00"),
                       pattern='.tif', all.files=TRUE, full.names=TRUE)

scene_4 <- list.files(here("data/hong_kong/landsat_8", "LC81220442015291LGN00"),
                       pattern='.tif', all.files=TRUE, full.names=TRUE)

# actually import each scene
s1 <- stack(scene_1)
s2 <- stack(scene_2)
s3 <- stack(scene_3)
s4 <- stack(scene_4)
```

``` r
names(s1) <- c("b1", "b2", "b3", "b4", "b5", "b6", "b7", "b10", "b11")
names(s2) <- c("b1", "b2", "b3", "b4", "b5", "b6", "b7", "b10", "b11")
names(s3) <- c("b1", "b2", "b3", "b4", "b5", "b6", "b7", "b10", "b11")
names(s4) <- c("b1", "b2", "b3", "b4", "b5", "b6", "b7", "b10", "b11")
```

``` r
scenes <- stack(s1, s2, s3, s4)
scenes_df <- as.data.frame(scenes)
```

``` r
lcz_and_scenes_df <- bind_cols(lcz, scenes_df)
```

``` r
names(lcz_and_scenes_df)[1] <- "lcz"
```

``` r
saveRDS(lcz_and_scenes_df, here("results", "hk_df.rds"))
```