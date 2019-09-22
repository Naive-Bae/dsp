[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Exercise: I started this book with the question, "Are first babies more likely to be late?" To address it, I computed the difference in means between groups of babies, but I ignored the possibility that there might be a difference between first babies and others for the same woman.

To address this version of the question, select respondents who have at least two live births and compute pairwise differences. Does this formulation of the question yield a different result?

Hint: use nsfg.MakePregMap:

`live, firsts, others = first.MakeFrames()`

`preg_map = nsfg.MakePregMap(live)`

`hist = thinkstats2.Hist()`
`later = 0`
`earlier = 0`
`same = 0`

`for resp, pregs in preg_map.items():`
    `if len(pregs) > 1:`
        `pair = preg.loc[pregs[0:2]].prglngth`
        `diff = np.diff(pair)[0]`
        `hist[diff] += 1`
        `if diff > 0:`
            `later += 1`
        `elif diff == 0:`
            `same += 1`
        `else:`
            `earlier += 1`

print("2nd child same", same)
print("2nd child earlier", earlier)
print("2nd child later", later)`

`2nd child same 1522
2nd child earlier 751
2nd child later 601`


`thinkplot.Hist(hist)
thinkplot.Config(xlabel='Difference (Weeks)', ylabel='Count')`

`pmf = thinkstats2.Pmf(hist)
pmf.Mean()`

-0.056367432150313125

