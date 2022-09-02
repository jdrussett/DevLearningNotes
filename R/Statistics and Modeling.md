# Statistics and Modeling

## General

---

### Basics/Summary Stats

- `Quantile()` takes numeric vector for one argument & returns min, max, 25th & 75th percentiles, & median
  - Can optionally receive another argument to specify custom quantiles
- `mean()` calculates mean
- `sd()` calculates standard deviation
- `var()` calculates variance
- `hmisc::wtd.quantile()` computes median of a column of a data set
- `favstats()` summarizes a variable from a data frame
  - Example: `favstats(~variable_name, data = data_frame)`
  - Good for one variable
- `mosaic::favstats(~column_name)` to get summary statistics on a column/variable
- `skimr::skim()` easily/quickly calculates some summary statistics of a variable it is passed
- `spread()` used with a contingency table will spread values of one column out into columns of their own
- Find factor-level means with `mean(~response_variable|factor_variable, data = data)`
- `confint()` provides a confidence interval for all coefficients on a model if a model object is passed
- Scale data into z-scores manually with the following code:

        for (i in 1:num_columns) {
            data[, i] <- (data[, i] - mean(data[, i]))/sd(data[, i])
        }

- `R2(data$predictions_var, data$response_var)` calculates an R-squared value for a model predicting a response variable from a data set
- `psycho::standardize()` calculates z-scores for all variables in a data set at once
- `coef()` when applied to a model will return its predicted coefficients
- `model.tables()` computes summary tables for model fits, especially complex analysis of variance model fits
- `prop.table()` creates a contingency table
  - Have to pass it a `table()` object

### Correlation

- `Cor()` computes correlation between variables in R
  - Make a plot:

        matrix <- cor(numeric_variables_of_data)
        corrplot(matrix) <-- not sure which library corrplot() is from

  - Alternatively, can make a plot with:

        data %>% PerformanceAnalytics::chart.correlation()

  - Will fail if there is any missing data in a column
    - Parameter `use = "complete"` will override problems with missing data
- `ggcorplot` library allows for more easily viewable correlation matrices
- `car::vif()` will auto-calculate variance inflation factor of a model
- `corrplot::corrplot()` creates a nice correlation visualization between all variables when you pass it a `cor()` object
- `PerformanceAnalytics::chart.Correlation()` produces a nice correlation matrix for a data set with graphs and R2 values

### Bootstrapping

- Creating bootstrap distribution:

      new_bootstrap_data <- original_data %>%
          rep_sample_n(size = n, reps = number_of_samples, replace = TRUE) %>%
          group_by(replicate) %>%
          summarize(mean(variable_of_interest))

- Function to get confidence interval from a bootstrap distribution is `get_confidence_interval()`
  - Set `type = 'percentage'` and `level = x` where x is the level of confidence you want (usually 0.95)
- Bootstrap distribution of sample proportion:

      bootstrap_distribution <- data %>%
        specify(response = categorical_variable_of_interest, success = category_of_success) %>%
        generate(reps = number_of_repetitions, type = 'bootstrap') %>%
        calcluate(stat = 'prop')

- Bootstrap distribution of sample mean:

      bootstrap_distribution <- data %>%
        specify(response = numerical_variable_of_interest) %>%
        generate(reps = number_of_repetitions, type = 'boot') %>%
        calcluate(stat = 'mean')

    > *Number of repetitions usually 1000*

- Bootstrapping sample means (different somehow?):

      boot_samp_means <- data %>%
        rep_sample_n(size = x, reps = y, replace = TRUE) %>%
        group_by(replicate) %>%
        summarize(sample_mean = mean(variable_of_interest))

- Bootstrap for sample mean (again?):

      null_distribution <- data %>%
        specify(response = response_var) %>%
        hypothesize(null = "point", mu = null_hypothesis_mean) %>%
        generate(reps = number_of_repetitions) %>%
        calculate(stat = "mean")

  - Can then run `visualize()` and `get_p_value()` commands
    - don't forget to include `obs_stat` and `direction` on that
- Plotting shaded confidence interval on a histogram:

      percentile_ci <- bootstrap_distribution %>%
        get_confidence_interval(level = x, type = "percentile")
      visualize(bootstrap_distribution) + shade_ci(endpoints = percentile_ci)

  - Where x is usually 0.95; can be adjusted to preference
- Bootstrapping for a difference in proportions:

      null_distribution <- data %>%
        specify(response,_var ~ x_var, success = "category_of_success") %>%
        hypothesize(null = "independence") %>%
        generate(reps = "number_of_repetitions") %>%
        calculate(stat = "diff in props", order = c("group1", "group2"))

  - To get p-value for sample statistic from null distribution:

        null_distribution %>% get_p_value(obs_stat = p1 - p2, direction = "right/left")

- Confidence interval for difference in proportions:

      bootstrap_distribution <- data %>%
        specify(response_var ~ x_var, success = "category_of_success") %>%
        generate(reps = number_of_repetitions, type = "bootstrap") %>%
        calculate(stat = "diff in props", order = c("group1", "group2"))

- Bootstrap for confidence interval of sample mean or sample standard deviation:

      i. bootstrap_distribution <- data  %>%
        specify(response = response_var) %>%
        generate(reps = number_of_repetitions, type = "bootstrap") %>%
        calculate(stat = "mean/sd")
      ii. bootstrap_distribution <- get_confidence_interval(type = "percentile", level = 1 - α)

### Distributions

*Model function defining prefix characters*:

| **Character** | **Description** |
| --- | --- |
| d | Calls density function for distribution; probability at a particular point |
| p | Calls cumulative density function for distribution; probability of any point before or at a particular point |
| q | Calls quantile density function for distribution; point at which a particular cumulative probability pertains (inverse of p) |
| r | Calls random generation function for distribution; generates random data according to a distribution |

- `_norm()` is normal distribution
  - Universal parameters are `mean =` and `sd =`
  - To find probability that a value is above a particular x-value you specify, modify command to `1 - pnorm()`
  - Can also use `xpnorm()` to get more information
- `_t()` is T distribution (decompressed normal distribution, according to degrees of freedom)
  - Universal parameter is `df =` and `ncp =`
- `_chisq()` is Chi-square distribution
  - Universal parameters are `df =` and `ncp =`
- `_unif()` is uniform distribution
  - Universal parameters are `min =` and `max =`
- `_pois()` is Poisson distribution
  - Universal parameter is `lambda =`
- `_binom()` is binomial distribution
  - Universal parameters are `size =` and `prob =`
- `_beta()` is beta distribution
  - Universal parameters are `shape1 =` and `shape2 =`
- `_gamma()` is gamma distribution
  - Universal parameters are `shape =`, `rate =`, and `scale =`
- `_nbinom()` is negative binomial distribution
  - Universal parameters are `size =`, `prob =`, and `mu =`

### Tests/Model Evaluation Techniques

- `get_p_value()` gets the p-value from a bootstrap distribution
  - `obs_stat` parameter is the desired sample statistic, direction can either left or right of HA
- *Performing a complete Chi-square test in R:*

        null_distribution <- data %>%
            specify(response = "response_var") %>%
            hypothesize(null = "point", p = c(
                "category1" = p1,
                "category2" = p2,
                "category3" = p3, ...
                )
            ) %>%
            generate(reps = number_of_repetitions, type = "simulate") %>%
            calculate(stat = "chisq")
        visualize(null_distribution)
        observed <- c(observed_values_of_categories)
        expected <- c(expected_values_of_categories) * sum(observed)
        chisq_sample <- sum(((observed - expected)^2)/expected)
        chisq_sample
        visualize(null_distribution) + shade_p_value(obs_stat = chisq_sample, direction = "greater")

- *Generating a QQ-plot:*

        data %>% ggplot(aes(sample = variable)) + stat_qq() + stat_qq_line()

- *Check a model's p-value with:*

        1 - pchisq(model_name$deviance, model_name$df.residual)

    > Reminder that low p-value indicates a bad fit for a poisson regression model

- `klaR::partimat()` provides a partition plot for a decision boundary for a linear discriminant analysis model
  - Pass it a formula, data source, and method just like you would `caret::train()`
- `twoClassSummary()` provides information like ROC, sensitivity and specificity for a categorical variable of interest in a data set (further research needed)
- Create ROC curves with `ROCR` library
- `vuong(model1, model2)` performs a Vuong test between two models
- `AIC()` calculates AIC of a model
- `t.test()` implements T test (hypothesis testing)
- `simulate()` will simulate a response from a distribution you pass it
- `lattice:qqmath()` draws quantile plots of a sample against a theoretical distribution, possibly conditioned on other variables
- `mosaic::tally()` will create a **confusion matrix** to evaluate a model's performance in predicting categorical membership of a response variable
  - Have to pass the function a formula, where the response variable `response_var ~ other_vars` is a variable created with the `predict()` function
  - Example:

        training_data <- training_data %>% 
            mutate(predicted_response = predict(response_var, type = ))
        confusion_matrix <- tally(predicted_response ~ other_vars, data = training_data)

  - Get classification accuracy with command `sum(diag(confusion_matrix))/nrow(training_data)`
- `randomForest::importance()` identifies the variables that are the most important in building decision trees for the random forest
  - Example:

        importance(random_forest_variable) %>% 
            as.data.frame() %>% 
            rownames_to_column() %>% 
            arrange(desc(MeanDecreaseGini))

- Use command `plot(varImp(bagged_tree_model))` to plot variable importance for a bagged tree model

### Modeling

- `aov()` generates analysis of variance model; construct just as you would a linear model
  - Example: `aov(response_var ~  factor_var, data = data)`
  - Set `aov()` equal to a variable, use `summary()` on it
- *Forward selection regression model:*

        model_name <- lm(response_var ~ 1, data = data_set)
        step(model_name, direction = 'forward', scope = (~ variable1 + variable2 + ... ))

  > Note: `lm(response_var ~ 1, data)` will regress the response variable against only an intercept; the "trivial" model

- *Backward selection regression model:*

        step(model_name, direction = 'backward')

- `leaps::regsubsets()` performs best subset selection model; finds best model for any subset of up to 8 variable
- `glm()` generalized linear model function can be used to specify non-linear forms of regression models
  - Use `family = "poisson"` to get a poisson regression model
  - Use `family = "quasipossion"` to get an over-dispersed poisson regression model
  - Use `family = "binomial"` to model a proportion (logit/probit)
    - Can specify link function with `family = binomial(link = link_function)` parameter
      - Available link functions are **logit**, **probit**, **cauchit**, **log**, or **cloglog**
      - If using log link function, have to pass a parameter start = c(coefficient_starting_points) with a starting point estimate for each coefficient and intercept
  - Use `family = "quasibinomial"` to model an over-dispersed proportion
  - Use `family = Gamma(link = link_function)` to make a Gamma response model with desired link function
    - Link functions include **log**, **inverse**, **identity**
- `pscl::zeroinfl()` generates a zero-inflation poisson regression model
  - A vertical bar `|` in a zero-inflation poisson model declaration indicates separation of explanatory variables in the poisson part from the zero-inflation part of the model
- `MASS::glm.nb()` generates a negative binomial regression model
- `predict()` will assign a prediction for a response variable based on a model
  - Use `predict()` if the value you want to predict is not a data point contained in the model
  - Use `model$fitted.values` if the value you want to predict is a data point contained in the model
  - Example: `predict(model_name, newdata = new_data)`
  - Add `type = "response"` parameter to the predict function if the prediction is made on the link scale and you want to predict on the response/data scale
- Can use `~ .` in model definition to indicate all remaining variables
- Can use `- variables` in model definition to indicate variables to omit from the model
- Include interaction terms in a model with `*` between two variables
- `anova()` creates an analysis of variance model to compare a trivial model to a nontrivial
  - Pass both models as parameters, and `test = "Chisq"` as the last parameter
- Any fitted model will have **residuals**, **fitted values**, and **coefficients**
  - Access these with the `$` operator
- `lme4::lmer()` creates mixed-effects model
  - Pass `response_var ~ (1|rand_fx_var)` argument to get random effects
  - Pass `variable1:variable2` argument to get fixed effects
- `lme4::ranef()` extracts conditional modes of random effects from fitted model object
- `model.matrix()` creates a design matrix for a model by expanding factors to a set of dummy variables
- `glmnet()` can be used to fit a ridge or lasso regression model
  - Adjust mixing with parameters `alpha =` and `lambda =`; when alpha = 1 and lambda = 0, lasso model, and when alpha = 0 and lambda = 1, ridge model
- `glmer()` specifies a model with fixed & random effects
  - Have to specify `weights =` variable parameter

### Training/Testing Splits

- `caret::createDataPartition()` used to create balanced splits into testing and training data sets
  - Example:

        train_index <- createDataPartition(data$response_var, p = [0, 1], list = TRUE/FALSE, times = number_of_partitions)

  > - `data$response_var` is target variable/output to classify
  > - `p` is a number between 0 and 1, percentage size of training set
  > - `list` is indicator of whether we want output to be in list format (usually want a `data.frame`, put FALSE)
  > - `times` is number of splits to create (usually leave it as 1)

  - Create training/testing sets out of the data using the `train_index` variable and bracket notation to select rows with and without the training index variable
- Use `sample()` to create general, not-necessarily-balanced training/testing splits of a data set (without caret)
  - Example:

        train_index <- sample(1:nrow(data), size = floor(percentage_size * nrow(data)))

  > - Where `percentage_size` is between 0 and 1
  > - Can also use `round()` instead of `floor()`

- Be sure to partition data set into training and testing manually after creating train or test index
  - Example:

        data_train <- data[train_index,]
        data_test <- data[-train_index,]

## Modeling with Caret

---

- Installing `caret` library needs dependencies:

      install.packages("caret", dependencies = c("Depends", "Suggests"))

- Model building with `caret::train()`:
  - Parameters needed are `formula`, `data`, `method`, & `family`
  - Example:

        model <- train(form = formula, data = data, method = "method", family = "family")

  - Options for method parameter include:
    - `"lm"` - basic linear regression model
    - `"lda2"` - linear discriminant analysis
    - `"glm"`
      - Options for family = parameter:
        - `"binomial"`
    - `"naive_bayes"`
    - `"qda"` - quadratic discriminant analysis
    - `"knn"` (for k-nearest neighbors model with `caret::train()`, also need to pass `tuneGrid` data frame parameter)
      - For plotting a knn model using `plot()`, can adjust metric plotting with `metric` parameter; from generic accuracy metric to Cohen's kappa metric
    - `"kknn"` (some kind of modified k-nearest neighbors? Minkowski distance?)
    - `"glmnet"` - lasso or ridge regression
    - `"rpart"` - decision tree
      - Can also optionally pass `tuneGrid` parameter, data frame, to force tuning parameters
      - If response variable is numeric, regression tree; if response variable is categorical, classification tree
    - `"treebag"` - bagged decision tree model
    - `"rf"` - random forest model
    - `"earth"` - MARS spline regression model (I don't know...)
    - Support vector machine methods:
      - `"svmLinear"`
      - `"svmRadial"`
      - `"svmPoly"`
  - View result with commands `model` or `summary(model)`
  - Make predictions for observations comprising the model based on its output and create a confusion matrix:

        data <- data %>% mutate(predictions_variable = predict(model))
        confusionMatrix(data = data$predictions_variable, reference = data$response_var)

  > - Save the confusion matrix as a variable and then use $table on that variable to access the confusion matrix's nice table

- `caret::trainControl()` implements cross-validation with caret
  - Set method parameter to select cross-validation type option:
    - `"boot"`
    - `"cv"`
    - `"LOOCV"` (leave-one-out)
    - `"LGOCV"`
    - `"repeatedcv"`
    - `"timeslice"`
    - `"none"`
    - `"oob"` (out-of-bag, only for random forest, bagged trees, etc.)
  - Set repeats parameter for number of repetitions
  - Implement a cross-validation method into a model with `caret::train()` by setting `trainControl()` equal to a variable, then pass that variable to the `trControl` parameter in `caret::train()`
- `caret::preProcess()` is caret's way of handling data preprocessing (i.e. centering & scaling)
  - Passing parameter `method = c('center', 'scale')` will center and scale data
  - Passing parameter `rangeBounds = c(0, 1)` will scale data to a [0, 1] scale
  - Passing parameter `method = c('pca')` will implement principal components analysis
    - To get testing/training sets

### Recipes

*Recipes in R:*

- `recipe()` builds a recipe:
  - Example:

            recipe_var <- recipe(response_var ~ explanatory_vars, data = data) %>%
                step_log(all_outcomes()) [or] step_BoxCox(all_outcomes())

- `all_outcomes()` and `all_predictors()` are both functions that can be used in recipes to apply a step to all outcomes or variables, respectively
- Use `caret::train()` to "cook" the recipe:
  - Example: `model <- train(recipe_var, data = data, method = "method")`
- Assessing predictions:
  - Example: `predictions_var <- predict(model, testing_dataset)`
- Prepping recipe:
  - Example: `recipe_trained <- prep(recipe_var, training = training_dataset, new_data = testing_dataset)`
- Baking recipe:
  - Example: `recipe_baked <- bake(recipe_trained, new_data = testing_dataset)`
- Evaluate predictions(?):
  - Example: `postResample(predictions_var = predict(model, testing_dataset), obs = recipe_baked$response_var)`
- Can add an extra step to impute missing values in a recipe with median values of the variable:
  - Example:

        recipe_var <- recipe(response_var ~ explanatory_vars, data = data) %>%
            step_log(all_outcomes()) [or] step_BoxCox(all_outcomes()) %>%
            step_medianimpute(column_name)

- `step_zv()` removes zero-variance features
- `step_nzv()` removes near-zero-variance features
- `step_center()` centers variables (can pass `all_predictors()`)
- `step_scale()` scales variables (can pass `all_predictors()`)
- `step_knnimpute()` applys a k-nearest neighbors (pass `all_predictors()` and `neighbors =` as parameters)

`caret::nearZeroVar(data, saveMetrics = TRUE)` checks data for non-informative variables/features

- Can achieve the same thing with a slightly more nicely formatted table with `kableExtra` library
  - Example:

        kableExtra::kable(nearZeroVar(data, saveMetrics = TRUE)) %>%
            kableExtra::kable_styling() %>%
            kableExtra::scroll_box(width = "100%", heigh = "500px")

## Advanced: Machine Learning Techniques

---

### Clustering

#### *Hierarchical*

- `hclust()` creates **hierarchical clusters** of data passed
  - Performing a `plot()` command on an `hclust()` object will return a **cluster dendrogram**
    - Other parameters to set include `hang =`, `cex =`, `label.offset =`
    - Passing data to function `as.phylo()` within plot command will rotate dendrogram
    - Passing `type = "fan"` will make fancy round plot out of cluster dendrogram
    - `tip.color = parameter` will color category name on dendrogram
- `cutree()` cuts a tree resulting from `hclust()` into several groups either by specifying cut height or desired number of groups

#### *K-Means*

- `mclust::kmeans()` creates **k-means clusters** on data
  - Parameters include `data`, `centers =`, and `nstart =`

### Principal Components

- `prcomp()` creates **principal components**
  - Always pass `center = TRUE`, `scale = TRUE`
- Each principal components model object has `$rotation` element, which gives the influence of each variable in each principal component

### Decision Trees

- `rpart::rpart()` fits a **decision tree** model
  - Same `formula =` and `data =` parameters as other model building approaches
  - Response variable has to be factor, by nature
- `rpart::printcp()` displays complexity parameter table for fitted decision tree model

### Random Forests

- `randomForest::randomForest()` is used to create **random forest model** (a collection of decision trees)
  - Same formula/data call method
  - Response variable has to be factor
  - `ntree =` parameter sets how many trees the forest will incorporate
  - `mtry =` parameter sets how many variables (randomly sampled) will be used as candidates to build each tree

### K-Nearest Neighbors Classification

- `class::knn()` defines a **k-nearest neighbors classification** model
  - Parameters include:
    - `data` - identifies data being passed into the model (duh)
    - `test` - identifies new observations to be tested/classified by the model
    - `cl` - specifies variable from data set upon which to base classification
    - `k` - specifies the number of neighbors to utilize to classify observations
    - `prob` - set to TRUE in order to have proportion of votes for the winning class to be returned as an attribute "prob"

### Neural Network (Single-Hidden-Layer only)

- `nnet::nnet()` fits single-hidden-layer neural network model
  - Pass normal model function as well as `size =` parameter, specifies number of units in hidden layer

## Deep Learning

---

- Learn more about deep learning in R at [Rstudio.com](https://keras.rstudio.com)
- R packages required for deep learning: `dplyr`, `keras`, `tfruns`, `tfestimators`, `TensorFlow`
- `keras::to_categorical()` creates a one-hot encoded matrix out of a multinomial response (required by `keras` for deep neural networks)
- keras::compile() incorporates back-propogation into a deep neural network
- fit() used for model training, parameters including batch_size, epochs, validation_spill, verbose
- layer_batch_normalization() applies batch normalization; adaptively normalizes data as mean/variance change over time during training; add after each middle layer within network architecture section of code
- regularize_XX() applies regularization; mitigates overfitting by placing constraints on model's complexity
- layer_dropout() adds dropout regularization method; randomly drops out a number of output features in a layer during training, helping prevent model from picking up on random patterns/noise; add between layers
- h20.deeplearning() creates/executes search grid; for hyperparameter tuning for DNNs
- tfruns::tuning_run() executes a tuning grid search; takes a long time, only assesses fraction of all models with adjustments for all tuning parameters)
- Probably never gonna use this shit, but some documentation of code available at:
  - file:///C:/Users/Jake%20Russett/OneDrive/Creighton%20Archive/MTH%20366/DeepLearn_snips.docx
  - file:///C:/Users/Jake%20Russett/OneDrive/Creighton%20Archive/MTH%20366/MTH366_HW9.html
