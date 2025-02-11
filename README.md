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

![Visualization](Project\images\Percent_for_skills.png)


### Insight

- Python is one of the most highly demanded and versatile skills for all of these three jobs.It eventually is the most demanded one for Data Scientist with 72%.
- Sql is also in the same boat as python as it is the most demanding skill in both Data Engineer with 68% and Data Analyst with 51%.
- Among those three,both Data Analyst and Data Scientist have almost the same skill-set requirement but Data Engineer has more technical skills requirement like in AWS or Azure.