Generic feedback to dataquest projects:

1. Write an intro - what is this project about, steps you're going to take, techniques, libraries you're using etc.
2. Conclusions, this is the most important part (though I like to leave it for the last moment in the middle 
of the night and do a terrible job of it). Some potentially very important people will skip the whole notebook and
**read only the conclusions at the very end**. So make them shine. Use of bold, lists etc. is a good way to organize and underline certain facts you want to share.
3. Merge cells that don't generate any output.
4. Don't comment too much - creating an empty list or dictionary doesn't require a comment line. Be efficient use 1 comment line per 2,3 or 10 lines of code
  
  example:
  ```
  # create an empty list:
  empty_list = []
  # loop trough something
  for thing in something:
    # for every green thing do a thing:
    if thing == 'green':
      new_thing = thing * 2
      # add to the list:
      empty_list.append(new_thing)
```
That was a lot of commenting, how about this one:
```
# find every green thing in something, multiply it by 2 and add to the list:
empty_list = []
for thing in something:
  if thing == 'green':
    new_thing = thing * 2
    empty_list.append(new_thing)
```
5. If you're generating plots - spend an extra few lines of code to make them nicer - it takes 1 line of code to make that plot bigger!
    * btw remember to us plt.show()
6. Use functions to reduce code. Eg. if you're generating the same plot every few cells, changing only the column name, maybe write a function for that? 
```
def function (df, colname):
  a = do some_plot_magic_here
  b = and_here
  c = some_more_magic
  return a, b, c 
  
 function (df,colname)
 plt.show()
 ```
7. If you're getting a 'SettingWithCopyWarning' you should do something about it, it doesn't look nice on a published notebook.
8. Remove double empty lines between the code lines, remove empty lines at the end of a cell.

9. To index or not to index? I say index, but it's a matter of personnal preference. Same goes to listing the libraries imports, different guides have different opinions:
    * [towardsdatascience](https://towardsdatascience.com/how-to-create-a-professional-github-data-science-repository-84e9607644a2
)
    * [dataquest](https://www.dataquest.io/blog/data-science-project-style-guide/)
10. At the end of the project (yeah we're back to that point) write a few lines about 
    * what have you learned
    * what are you planning to do in the future (but now you're missing time/ skills)
    * what you've tried but didn't work and it wasn't included in the final version (different approach/ new library?)
11. Don't try to tick the box with your project, **try to make it the best project.** I know it's hard you may be at the beginning of the course, maybe this, maybe that. But... 
    * find something that no one has done before, and do it. 
    * Not enough data? Get more! 
    * Data is boring and can't find anything interesting? Roll up your sleeves and create the best visualizations you can. 
    * Out of ideas/ not enough skills? Attach a cute photo of your dog (sorry no cats allowed). 
    * **Make them remember your project.**
