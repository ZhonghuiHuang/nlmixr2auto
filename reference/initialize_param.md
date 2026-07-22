# Initialize model parameters from parameter table

Generates parameter initialization code based on a parameter table,
handling both fixed and estimated parameters.

## Usage

``` r
initialize_param(param_name, param_table)
```

## Arguments

- param_name:

  Character, name of the parameter to initialize (without "l" prefix)

- param_table:

  Dataframe containing parameter specifications, must include:

  - `Name`: Character parameter names with "l" prefix (e.g., "lka"
    corresponds to param_name="ka")

  - `init`: Numeric initial values

  - `fixed`: Integer flag (0/1) indicating fixed status (1 = fixed)

## Value

Character vector containing generated initialization code line. Format:

- Fixed parameters: `<param_name> <- fix(initial_value)`

- Estimated parameters: `l<param_name> <- initial_value`

## Author

Zhonghui Huang

## Examples

``` r
# Create sample parameter table
param_table <- initialize_param_table()

# Generate initialization code
initialize_param("ka", param_table)  # Returns "ka <- fix(0.500)"
#> [1] "lka <- 1.0"
initialize_param("cl", param_table)  # Returns "lcl <- 1.200"
#> [1] "lcl <- 1.0"
```
