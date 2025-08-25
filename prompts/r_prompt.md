when coding in R,

* I don't need much explanation of code.
* Spread long function calls across multiple lines.
* Where needed, always indent function calls with two spaces.
* Only name arguments that are less commonly used.
* Always use double quotes for strings.
* Use the base pipe, `|>`, not the magrittr pipe `%>%`.
  
- use `list2env(c(parms, as.list(state)), envir = environment())` inside the ODE model, not parms$ParameterName wgich gives NULL as silent error..
- use parms as often as possible for aprameter bojects in various functions, not par or pars.
- don't use `t` as object name, it is for transposing a matrix in base R. 
- call the time column of the resulting data.table `time`, not `time_d`etc
- use the `<-` assignment rather than `=`
- don't use the '<<-' operator, unless it make sense, in which case Notify and Explain to me.
- write out greek symbols in generated code (in explanations ok), and in units, use prefix `u` instead of `\mu` for 'micro'.
- do not use T as an object (e.g. for Temperature or anything else) since it stands for TRUE
- please use data.table rather than tidyverse if possible. ggplot2 is great though. 
- if possible, avoid matrix objects, make data.tables, with proper column names
- don't use greek symbols (difficult to type, send); if original authors used it, write  'alpha_0' etc.
- for ODE models, please  use deSolve; add initial states to the list of parameters, add units for all states / parameters in the comments.
- when integrating with the function deSolve::ode, use , method = "rk4" explicitly
- for deSolve::ode() function, please make sure the names of initial conditions y are the same as the names of the states in the model, and that the order of the states in the initial conditions vector is the same as in the model.
- when creating the vector initial_states for a state `a`, make sure the par$steady_state_a or event$time is unnamed first! (or the name of the initial state will be corrupted).
- Note that in ggplot2, the size` aesthetic for lines was deprecated, use `linewidth` instead

- Check that almost all functions get their info passed as arguments, unless there are globals on purpose (which can be fine!)


IMPORTANT (read carefully, ask if not clear)

When calling R functions, follow these naming rules:

- If the object name exactly matches the parameter name, naming the argument is optional
- If the object name differs from the parameter name, the argument MUST be named  
- Once any argument is named in a function call, name all subsequent arguments
- Exception: trailing arguments with defaults can remain unnamed

EXAMPLES
- For function: create_S_matrix(sensitivity_dt, normalization = "parameter_relative")

- Correct: create_S_matrix(sensitivity_dt = sensitivity_results, normalization = "parameter_relative") 
- Incorrect: create_S_matrix(sensitivity_results, normalization = "parameter_relative")

For function: f(data, method = "default", verbose = TRUE)

- If object is named 'data': f(data, method = "custom") ✓
- If object is named 'my_data': f(data = my_data, method = "custom") ✓
- Never: f(my_data, method = "custom") ✗



- If you want to assign the value of a variable named field from the environment to the column field, do:
`dt[, field := ..field]` not `dt[, field := field]` which is meaningless.


e.g.
for a function defined
`f <- function(a, b = 1, c = 2, d = 3){...} ;`
call it as
`a <- 5; bprime <- 11 ; c <- 22 ; x <- f(a, b = bprime, c = c)`

- before each "for loop" please add one line with the runner initialized to the first element, for debugging: e.g.
# For each meal pattern and size factor

```r
pattern <- "three_meals"  # <-- add this line for debugging
for (pattern in c("three_meals", "one_meal")) {
factor_idx  <- 1 # <-- add this line for debugging
for (factor_idx in 1:length(meal_size_factors)) { ... } }
```

- when NOT in a shiny app, and generating multiple ggplot2 plots (named p1, p2, etc. or whatever), please also add these to a list called pList(p1 = p1, p2 = p2, ...) etc. Initialize such a script with pList <- list() at start of a run script, or a run_all() type of function, and then return that pList object in the results.

- when creating excel files from R with openxlsx::createStyle() note that `border = c("all")` is deprecated, should be `border = c("top", "bottom", "left", "right")`
- also within openxlsx, addStyle does not take both rows and cols in ranges thus, as example, this 
`addStyle(wb, "xxx", calc_style, rows = 2:3, cols = 1:5)
should be
`lapply(2:3, \(rr) addStyle(wb, "xx", calc_style, rows = rr, cols = 1:5))
- and finally be careful with writing headers data.tables to excel (not (over)writing them twice.)

- put simulation code in separate functions from visualization code


When building Shiny apps, extract all significant computational logic into standalone functions that take explicit parameters, then wrap them in thin reactive layers. Use this pattern:

```r # Standalone function - testable, debuggable, reusable
my_computation_fun <- function(input_params) {
  # All logic here with clear inputs/outputs  
  # Add unit comments: [m], [s], [kg], etc.
  return(result)
}

# Thin reactive wrapper
my_computation <- reactive({ 
  my_computation_fun(input) 
})
```

This makes code testable with my_computation_fun(test_params), debuggable with breakpoints, and reusable across contexts. Always include unit comments and clear parameter contracts.



Shiny Development Rules: Build Smart, Not Complex

- Start with static plots using ONE technology (ggplot OR plotly) - get basic visualization working before any interactivity
- Add manual controls first (sliders, buttons) - never attempt automatic animations until manual control works perfectly
- When something breaks, SIMPLIFY rather than add complexity - strip back to last working version, don't pile on reactive logic
- Use minimal data for prototyping (10-20 frames, 50 points max) - optimize performance only after functionality works
- Test each feature independently - plotting, then controls, then physics, then polish - one working piece at a time

