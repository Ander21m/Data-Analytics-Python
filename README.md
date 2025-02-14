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





## 2.How Well do jobs and Skills pay for Data Analyst???


### VIsualize Data

```python


sns.boxplot(data=df_us_top6,x ="salary_year_avg",y="job_title_short",order=job_order)
sns.set_theme(style="ticks")
plt.title("Top 6 Jobs and their salary in the United States")
plt.xlabel("Yearly Salary ($USD)")
ax = plt.gca()
plt.ylabel("")
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos:f"${int(x / 1000)}K"))
plt.xlim(0,600000)
plt.show()
```


### Results

![Visualization](Project/images/Salary_For_Top6_in_US.png)


### Insight


- The Senior role of each respective jobs pay higher than that of junior or entry level role.But Senior role for Data Analyst is lower than the junior or entry level role of Data Engineer and Data Sceintist.


### Highest Paid and Most demanded Skills for Data Analyst in US


### VIsualize Data

```python
fig,ax = plt.subplots(2,1)

sns.set_theme(style= "ticks")

#df_DA_Us_Toppay[::-1].plot(kind = "barh",y = "median",ax= ax[0],legend= False)
sns.barplot(data= df_da_top_pay,x = "median",y = df_da_top_pay.index,ax = ax[0],hue= "median",palette="dark:b_r")
ax[0].set_title("Top 10 Highest Paid Skills for Data Analysts")
ax[0].set_ylabel("")
ax[0].set_xlabel("")
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos:f"${int(x / 1000)}K"))
ax[0].legend().remove()

#df_DA_Us_skills[::-1].plot(kind = "barh",y = "median",ax= ax[1],legend = False)

sns.barplot(data= df_da_top_jobs,x = "median",y = df_da_top_jobs.index,ax = ax[1],hue ="median",palette="light:b")
ax[1].set_title("Top 10 Highest Paid Skills for Data Analysts")
ax[1].set_ylabel("")
ax[1].set_xlabel("Median Salary (USD)")
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos:f"${int(x / 1000)}K"))
ax[1].set_xlim(ax[0].get_xlim())
ax[1].legend().remove()

plt.tight_layout()
plt.show()
```


### Results

![Visualization](Project/images/Top_paid_and_most_deman_for_da_in_Us.png)




### Insight


- The top graph shows specialize technical skills like `dplyr`,`bitbucket` and `gitlab` are paid really high reaching to around and over 175K per year.

- The bottom graph shows that skills like `python`,`tableau` and `r` are paid the highest among the most demanded skills.





### VIsualize Data

```python
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter


#df_plot.plot(kind ="scatter" ,x ="skill_percent",y= "median_salary")
sns.scatterplot(data=df_plot,x= "skill_percent",y ="median_salary"
                ,hue="technology")

sns.despine()
sns.set_theme(style="ticks")

texts =[]
for i,text in enumerate(df_plot["skills"]):
   
    texts.append(plt.text(df_plot["skill_percent"].iloc[i],df_plot["median_salary"].iloc[i],text))

adjust_text(texts,arrowprops =dict(arrowstyle = "->",color ="gray",lw= 1))   

ax =plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y,pos:f"${int(y/1000)}K"))
ax.xaxis.set_major_formatter(PercentFormatter(decimals= 0))

plt.xlabel("Percent of Skills in Jobs")
plt.ylabel("Median Yearly Slary")
plt.title("The Most Optimal Skills for Data Analyst in US")
plt.tight_layout()
plt.show()
```


### Results

![Visualization](Project/images/Most_Optimal_Skills_For_DA.png)




### Insight


- The Programming language like python and sql are most optimal and also most paid skills for data analyst jobs.

- Analyst Tools such as excels and tableau are also relatively high in demand.Tableau has much higher salary tahn excel according to this graph.

-Other skills like database and cloud are not that in demand.But they are paid a really good amount of salary e.g. cloud related jobs like oracle is the second highest paid job after python in this graph.

