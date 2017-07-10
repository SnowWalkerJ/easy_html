# easy_html

easy_html is a simple module that help quickly build html file with python.

## installing

This module doesn't require installing. Simply copy the file to your project path and install the required packages, and you are ready to go!

## Usage

### Basic Usage

The basic usage of easy_html is just like writing html. Use context manager to control the opening/closing of the tags. Below is an example.

```python
from easy_html import HTML
h = HTML()                                 # create an HTML document
with h.use(h.body):                        # everything we do is under body
    with h.div(_class="row"):              # a new div with class="row"
        h.inline("h1", _text="Title")      # title
        h.inline("hr")
    with h.div(_class="row"):
        h.inline("a", href="http://www.github.com", _text="Click me")

print(h.render())
```

This will generate html code as below:
```html
<html>
 <head>
   <meta charset="utf-8"></meta>
   <meta content="width=device-width, initial-scale=1" name="viewport"></meta>
   <link type="text/css" rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"></link>
   <link type="text/css" rel="stylesheet" href="https://pingendo.github.io/templates/blank/theme.css"></link>
 </head>
 <body>
   <script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/tether/1.4.0/js/tether.min.js"></script>
   <script src="https://pingendo.com/assets/bootstrap/bootstrap-4.0.0-alpha.6.min.js"></script>
   <div class="row">
     <h1>Title</h1>
     <hr></hr>
   </div>
   <div class="row">
     <a href="http://www.github.com">Click me</a>
   </div>
 </body>
</html>
```
By default, easy_html refers to static files for jQuery and Bootstrap.


## Something Awesome

As you may noticed, this style of building html is quite boring.
So we designed something different for you.

```python
t = pd.DataFrame(
    np.random.randn(4, 4),
    columns=["c1", "c2", "c3", "c4"]
)
h = HTML(enable_highcharts=True)
with h.use(h.body):
    h.inline("h1", _text="Title")
    h.inline("hr")
container = h.container()
row = h.row(container)
c1, c2 = h.col(row, [6, 6])    # creates two columns in a row, split the screen half-half.
with h.use(c1):
    h.generate_table(t)        # generate the table on the left
with h.use(c2):
    h.highcharts("Chart", t)   # plot it with highcharts on the right
print(h.render())
```

Output:
```html
<html>
  <head>
    <meta charset="utf-8"></meta>
    <meta name="viewport" content="width=device-width, initial-scale=1"></meta>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet" type="text/css"></link>
    <link href="https://pingendo.github.io/templates/blank/theme.css" rel="stylesheet" type="text/css"></link>
  </head>
  <body>
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/stock/modules/exporting.js"></script>
    <script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tether/1.4.0/js/tether.min.js"></script>
    <script src="https://pingendo.com/assets/bootstrap/bootstrap-4.0.0-alpha.6.min.js"></script>
    <h1>Title</h1>
    <hr></hr>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <table class="table table-hover table-bordered">
            <thead>
              <tr>
                <th>#</th>
                <th>c1</th>
                <th>c2</th>
                <th>c3</th>
                <th>c4</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>0</td>
                <td>-0.20</td>
                <td>0.24</td>
                <td>1.84</td>
                <td>1.41</td>
              </tr>
              <tr>
                <td>1</td>
                <td>0.46</td>
                <td>-0.69</td>
                <td>0.40</td>
                <td>1.46</td>
              </tr>
              <tr>
                <td>2</td>
                <td>0.47</td>
                <td>0.84</td>
                <td>-1.22</td>
                <td>-0.23</td>
              </tr>
              <tr>
                <td>3</td>
                <td>-0.32</td>
                <td>1.57</td>
                <td>0.44</td>
                <td>-0.94</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="col-md-6">
          <div id="highcharts-Chart"></div>
          <script>
            Highcharts.chart('highcharts-Chart', {"series": [{"tooltip": {"valueDecimals": 3}, "name": "c1", "data": [-0.31699030142854623, -0.19920669562530138, 0.4642984624005802, 0.46570426719777414], "type": "line"}, {"tooltip": {"valueDecimals": 3}, "name": "c2", "data": [-0.6874100023606234, 0.23616310712789926, 0.8352679492902365, 1.5675330083785308], "type": "line"}, {"tooltip": {"valueDecimals": 3}, "name": "c3", "data": [-1.2208659937966237, 0.39509162417847, 0.4417390212605732, 1.8436423086892], "type": "line"}, {"tooltip": {"valueDecimals": 3}, "name": "c4", "data": [-0.9378052637051875, -0.23279546382135421, 1.4051923967078404, 1.4591743462239277], "type": "line"}], "title": {"text": "Chart"}, "xAxis": {"type": "linear"}});
          </script>
        </div>
      </div>
    </div>
  </body>
</html>
```

Copy these in your python environment and see the result yourself!
