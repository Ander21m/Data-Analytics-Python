# The Analysis


## 1. What are the most demanded skills for the top 3 most popular data roles?


To find the most demanded skills for the top 3 most poplular data roles.First, I filtered out those positions by which ones are the most popular.Then i got(retreived) top 5 skills for these top 3 roles.The query i provided here represent and highlight the most popular job titles and their job skills.Additionally,it also gave me some insights about which skills should i pay attention to depending on the role I'm targeting.


View my notebook with detailed steps here:

[2.Skills_Count.ipynb](Project/2.Skills_Count.ipynb)

### Visualize Data

```pythonimport seaborn as sns

fig,ax = plt.subplots(len(job_title),1)
sns.set_theme(style="ticks")
for i,jt in enumerate(job_title):
    df_plot = df_skill_perc[df_skill_perc["job_title_short"] == jt].head(5)
    
    sns.barplot(df_plot,x="skill_percent",y = "job_skills",ax = ax[i],hue ="skill_count",palette="dark:b_r")
    ax[i].set_title(jt)
    ax[i].set_ylabel("")
    ax[i].set_xlabel("")
    ax[i].get_legend().remove()
    ax[i].set_xlim(0,78)

    for j,value in enumerate(df_plot["skill_percent"]):
        ax[i].text(value + 1,j,f"{value:.0f}%",va ="center")
    if i != len(job_title)-1 :
        ax[i].set_xticks([] )

fig.suptitle("Percent of Skills to be Requsted in US Job Posting",fontsize= 15)
fig.tight_layout(
    h_pad=0.5
)
plt.show()
```

### Results

![Visualization](Project/images/Percent_for_skills.png)


### Insight

- Python is one of the most highly demanded and versatile skills for all of these three jobs.It eventually is the most demanded one for Data Scientist with 72%.
- Sql is also in the same boat as python as it is the most demanding skill in both Data Engineer with 68% and Data Analyst with 51%.
- Among those three,both Data Analyst and Data Scientist have almost the same skill-set requirement but Data Engineer has more technical skills requirement like in AWS or Azure.

## 2.How are in-demand skills trending for Data Analysts??

### VIsualize Data

```python


from matplotlib.ticker import PercentFormatter

df_plot = df_da_Us_percent.iloc[:,:5]

sns.lineplot(data= df_plot,dashes= False,palette= "tab10")
sns.set_theme(style= "ticks")
sns.despine()
plt.title("Trending Top Skills for Data Analysts in the US")
plt.ylabel("Likelihood in Job Posting")
plt.xlabel("2023")
plt.legend().remove()

ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals= 0))
for i in range(len(df_plot.columns)):
    plt.text(11.2,df_plot.iloc[-1,i],df_plot.columns[i])

plt.show()
```


### Results

![Visualization](Project/images/Percent_of_Likelihood_For_DA.png)


### Insight


- Sql is most demanded at the start of the year with over 60%.The likelihood(demanding) for Sql is decrease a bit around Jue and July and for the rest of the year the graph looks steady.

- Python is 4th most demanded skills of Data Analyst as we can see.But in the month like June,August and November Python has nearly the same percentage for likelihood as the 3rd place tableau.Eventually, at the end of the year,in between November and December Python becomes thrid most demanded skills.