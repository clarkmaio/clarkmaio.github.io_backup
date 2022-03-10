# DataExplorer: a prototype
Ok this is the story. I've once red about this very cool product by [einblick](https://einblick.ai/).

It is a tool to dynamically explore data and even fit simple models. It is very useful during the development phase of a project.

Namely when you are studying a new dataset you would like to be free to explore relations between all the variables and find patterns. A good way to do it is to visually approach data (*i.e. plot everything*) and later analytically (*i.e. feature selection, try to make some regression...*).


I've tried to write a prototype (not even close to **einblick** product) that let me explore a pandas dataframe in a very fast and easy way.

In **clark_py/dash/data_explorer.py** (*see [clark_py](https://github.com/clarkmaio/clark_py)*) you will find **DashDataExplorer** class.
Suppose you have a dataframe **df** you want to explore then you can run:
    
    from clark_py.dash.data_explorer import DashDataExplorer
    import plotly.express as px
    import panda as pd
    
    # build dataframe to explore
    df = px.data.iris()
    df['valuedate'] = pd.date_range(datetime(2021, 1, 1), datetime(2021, 1, 1) + timedelta(days=len(df)-1), freq='D')

    dde = DashDataExplorer()
    dde.run(df, debug=True)


The result is a dashboard with modules in which you can build on the fly plots using values of **df** dataframe.


In each module (in this prototype there are just 2 modules...in the future the modules will be dynamically built) you can specify:
* **plot type**
* **width**
* **height**

![screen_1](https://raw.githubusercontent.com/clarkmaio/clarkmaio.github.io/main/img/data_explorer/screen_shot_1.PNG)

**width** and **height** are parameters just to set plot dimension. Let's focus on the first parameter.
You can choose between:

* scatter
* scatter matrix (*pairplot in seaborn*)
* timeseries
* 2timeseries

Depending on what you choose a second set of parameter to be selected will appear.

For example if you choose *scatter* you have then to choose:
* x axis variable
* y axis variable
* hue variable (*optional*)
* size variable (*optional*)
* regression line switch (*optional*)

 ![screen_2](https://raw.githubusercontent.com/clarkmaio/clarkmaio.github.io/main/img/data_explorer/screen_shot_2.PNG)



Another example is **scatter_matrix** mode which is equivalent to *seaborn pairplot* and let you visualize multiple scatter plots at once to compare relations between variables.


![screen_3](https://raw.githubusercontent.com/clarkmaio/clarkmaio.github.io/main/img/data_explorer/screen_shot_3.PNG)
![screen_4](https://raw.githubusercontent.com/clarkmaio/clarkmaio.github.io/main/img/data_explorer/screen_shot_4.PNG)

