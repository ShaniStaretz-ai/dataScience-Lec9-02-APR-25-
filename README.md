# dataScience-Lec9-02-APR-25-
GROUP BY presentation 22 start from page 4
* df.ffill()- forword fill()
* df.bfill()- backwords fill()
* df.groupby(<label>)- return generic structure - not easy to work with, need to convert to some struction
  * template: groupby(column name).<column to do the action>.<what action to do-function>(numeric_only=True- do the action only on numbers)
  * df.groupby('model_year')[weight].mean()=the index is model year value and the values :
    *  for each model_year return the result calculation of mean on all weight
    * in a list :df.groupby('model_year')[weight].mean()
    * in a df: df.groupby('model_year')[[weight]].mean()
    * in a df: df.groupby('model_year')[[weight],'mpg']].mean()= will do for each model_year mean for weight and mean for mpg
  * df.groupby('model_year')[weight].value_counts()- for each year count each weight
  * df.groupby('model_year').value_counts()- for each group do the action value_count for each column
  * df.groupby('model_year').agg({})- page 11: to make different action on different columns 
    * df.groupby('model_year').agg({'weight':'max'/['max','min'],mpg:'mean'}).rename(columns={weight:max_weight,mpg=mean_mpg})- 
    * better to do rename on the columns- to the results of the actions in the agg
  * groupby makes the element to be the index - if want to make after action, better to reset_index()
  * df.groupby('model_year')['horsepower'].nlargest(3)= return the top 3 max values and their index number
    * 70 group_year 8 index 225 values
  * group by 2 columns ['model_year', 'cylinder']: multi indexing
    * groupby_year=df.groupy(['model_year', 'cylinder']).value_counts: return for each group, how many have year=70 and cylinder= 4
    * index is a list of tuples: the to access need use tuple:loc[(71,4)]
      * if you do reset index, indexes columns become columns
     
    * can return by first index[71]
    * can't return all loc[(:4)]- by second index
      * therefore use: cross_Section: xs:  without change the structure
        * groupby_year.xs(level='cylinders',key =4)
        * if want by 2 value cylinders 6,8:
          * or filter by cylinders and the groupby
            * ![img.png](img.png)
          * or swaplevel to 4,70 and the loc[4]
            * df.swaplevel vs xs: swaplevel more expensive and not ideal
              * then you can sort_index(level=['cylinder','model_year'])
  * concat - by row/by column
  * merge(df1,df2,left_on=label,right_on=lebal,suffixes/how)
    * suffixes =  merge df and add suffixes on duplicate columns
    * how= default=inner join, options:inner,left,right, cross
  * str methods: .str.<str function> 
    * works on values/ columns
    * to replace apply with cb function
  * time methods: pd.to_datetime(df['DATE']):
    * works good with groupby, to get all groups by month from the full date
    * format='dd-mm-yyyy'
    * resample(rule='A')- create group by rule A= like create group by month/day/year and then continue with groupby actions