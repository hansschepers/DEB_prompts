When writing MATLAB code with multiple functions, always use the function handle approach to avoid file structure issues:

**MATLAB Function Handle Structure Rules:**

1. **Main function returns struct of handles** - First function returns `struct()` containing `@function_name` handles to all subfunctions
2. **No script code after functions** - Only function definitions after the main function, never standalone script lines
3. **Single file solution** - All functions in one .m file, accessible via handles
4. **Clear usage pattern** - Show how to get handles and call functions

**Template Structure:**
```matlab
function handles = main_function_name()
handles = struct();
handles.main_task = @main_task;
handles.helper1 = @helper1;
handles.helper2 = @helper2;

fprintf('Usage: h = main_function_name(); h.main_task();\n');
end

function main_task()
% Main functionality here
end

function result = helper1(input)
% Helper function 1
end

function result = helper2(input)
% Helper function 2
end
```

Always include:

- Usage examples in comments/fprintf
- Clear function handle names
- Demonstration function for quick testing
- No script code below function definitions


When writing MATLAB code, follow these R-inspired organizational principles:

**MATLAB Library Organization:**

- Create personal utilities in separate files (personal_utils.m)
- Always use consistent object names: utils = personal_utils()
- Document dependencies clearly in analysis files
- Use utils.function_name() syntax (R package-like)
- Include mget_ls() and other R-inspired utilities in personal_utils
- Keep domain-specific functions (DEB, etc.) in separate libraries


**MATLAB Function Structure (R-like Style):**

1. **Function handle approach** - Main function returns struct with handles to all subfunctions
2. **Comprehensive returns** - Functions return complete structured outputs (R list-like behavior)
3. **R-like variable access** - Use result.variable_name syntax for all outputs
4. **Include mget_ls() equivalent** - Capture all local variables in returned structure

**Template Structure:**
```matlab
function handles = main_analysis()
    handles = struct();
    handles.run_analysis = @run_analysis;
    handles.helper_func = @helper_func;
    
    fprintf('Usage: h = main_analysis(); result = h.run_analysis();\n');
end

function output = run_analysis()
    % Analysis code here
    params = get_params();
    results = do_analysis();
    
    % R-like comprehensive return
    output = struct();
    output.params = params;
    output.results = results;
    output.metadata = struct('date', datestr(now), 'version', version);
    output.summary = struct('key_stat', some_value);
    
    % R-like utility functions
    output.list_vars = @() fieldnames(output);
    output.get_all = @() output;
end
```

Key Principles:

- Return comprehensive structs instead of using assignin()
- Provide R-like list access patterns: result.item
- Include metadata and summary statistics
- Make functions self-contained with clear interfaces
- Use parameter-relative normalization for sensitivity analysis
- Include biological units and dimensions in comments
- Follow mathematical rigor with real-world applications

For sensitivity analysis specifically:

- Use parameter-relative normalization: (∂y/∂p)*p
- Create S matrices for parameter covariance analysis
- Include both raw and physical outputs with proper units
- Provide correlation analysis and PCA without requiring toolboxes
