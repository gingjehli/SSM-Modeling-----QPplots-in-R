# SSM-Modeling-----QPplots-in-R
This R code serves as a template to create quantile-probability plots in R

I'm just providing the code in the attached script that needs to be modified based on the number of task conditions etc.
To see an example of how the Quantile Probability Plot looks like, see here:
http://rpubs.com/gingjehli/975992


For interpreting a Quantile-Probability plot:
Quantile probability plots simultaneously display response frequencies (along the x-axis) and quantiles of reaction times (along the y-axis) that approximate the entire RT distribution for each response frequency. This allows a more detailed investigation of the data and displays the relationship of response frequencies and RTs directly within one plot. The x-axis represents the response frequency of each response type and for each task condition (represented by different symbols and colors that are explained below). Response frequency of 0.5 means that people chose that given response option half the time. Along the y-axis are the RT quantiles (i.e., the 0.1, 0.3, 0.5, 0.7, and 0.9 quantile RTs) vertically plotted from bottom to top respectively.
In the plot above:
1. the four colors represent the four different task conditions - one for each of the evidence conditions (see definition on top of the script). 
2. Filled symbols represent the frequency of responses towards the upper boundary (in this case: "approach decisions"). Non-filled symbols represent the frequency of responses towards the lower boundary (in this case: "avoidance decisions").

Note:
You always want to compute the RT-quantiles for each individual separately and then average across individuals. This is important because mathematically, taking the means of numbers is a non-linear operator (i.e., the order of operations matters).
There are some more details about this to find here:

Ratcliff, R. (1979). Group reaction time distributions and an analysis of distribution statistics. Psychological bulletin, 86(3), 446.
