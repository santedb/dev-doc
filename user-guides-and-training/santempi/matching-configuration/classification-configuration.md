# Classification Configuration

The classification tab of the match configuration screen allows administrators the opportunity to view and edit the thresholds and method of classification for any results which have been scored in the scoring stage.

![](<../../../.gitbook/assets/image (95).png>)

The screen shows the thresholds at which a candidate `$block` record will be classified as a match, non-match or probable match.

## Editing Classification

Pressing the edit button on the classification panel will enable sliders for modifying the classification thresholds.

![](<../../../.gitbook/assets/image (376).png>)

The administrator may select an evaluation mode which can be one of:

* Classification via Absolute Score - This method of scoring (the default) will sum all the outputs of each attribute configured in the scoring part of the match process. This is useful if the `ignore` statement is not used in your configuration and allows for thresholds to be set using the range `-minScore ... +maxScore` .
* Classification via Normalized Score - This method of scoring will normalize the `$block` score to only those attributes which were evaluated (i.e. not ignored or removed) as a number between `0..1` . This is useful for datasets where data may be missing and attributes are excluded. The calculation of normalizing the score is $$score=\frac{score + abs(minScore)}{maxScore + abs(minScore)}$$
