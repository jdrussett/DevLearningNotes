# Modeling

## Basics

---

`scipy.stats.linregress()` function takes `x` and `y` arguments & creates simple linear regression equation

`.corr()` method on a dataframe will calculate correlation coefficients for the numerical variables & output correlation matrix

`pearsonr()` (Pearson correlation coefficient function) takes two arguments (arrays or dataframes) & outputs Pearson correlation coefficient & correspondign two-tailed p-value

Multiple regression model example:

    import statsmodels.formula.api as smf
    dataframe_variable = pandas.read_csv('[dataframe csv file]')
    multiple_regression_model = smf.ols('y ~ x1 + x2 + x3 … + xn', dataframe_variable).fit()
    multiple_regression_model.summary()

`ANOVA` model/table example:

    from statsmodels.formula.api import ols
    import statsmodels.api as sm
    dataframe_variable = pandas.read_csv('[dataframe csv file]')
    model_variable = ols('y ~ x1 + x2 + x3 … + xn', dataframe_variable).fit()
    anova_table_variable = sm.stats.anova_lm(model_variable, typ = 2)

Numpy data transformation functions (if x is a dataframe or array variable):

- `numpy.log(x)` takes logarithm of `x`
- `numpy.square(x)` squares `x`
- `numpy.sqrt(x)` takes the square root of `x`
- `numpy.exp(x)` exponentiates `x`
