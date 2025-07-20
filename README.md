%% ===================== ECM MODEL INPUT SETUP ============================
% This code prepares all necessary variables to be used in Simulink:
% - SOC_input and Temp_input are time-varying signals (via From Workspace)
% - R0_LUT, R1_LUT, C1_LUT, R2_LUT, C2_LUT are static 2D lookup tables
% - SOC_bp and Temp_bp are the breakpoints for the lookup tables

%% 1. Define Breakpoints
SOC_bp = [0.05 0.15 0.25 0.35 0.45 0.55 0.65 0.75 0.85];  % Midpoints of 9 SOC regions
Temp_bp = [29.5 30.4 31.2 31.4 31.7 31.8 31.9 32.5 33.0 33.8];  % 10 temperature values

%% 2. ECM Values from Your Table (per SOC region)
R0_vals = [0.0008 0.0012 0.0012 0.0012 0.0012 0.0012 0.0012 0.0014 0.0014];
R1_vals = [0.0011 0.0010 0.0009 0.0009 0.0010 0.0012 0.0012 0.0011 0.0011];
C1_vals = [30506.1 31132.8 28978.6 28077.2 30410.7 32308.6 28028.0 29204.8 31794.4];
R2_vals = [0.0005 0.0004 0.0005 0.0005 0.0004 0.0005 0.0005 0.0005 0.0006];
C2_vals = [34084.4 38227.7 34895.8 34886.6 35707.0 34720.7 33459.9 35271.3 35678.5];

%% 3. Expand ECM values across temperatures (replication)
R0_LUT = repmat(R0_vals', 1, length(Temp_bp));
R1_LUT = repmat(R1_vals', 1, length(Temp_bp));
C1_LUT = repmat(C1_vals', 1, length(Temp_bp));
R2_LUT = repmat(R2_vals', 1, length(Temp_bp));
C2_LUT = repmat(C2_vals', 1, length(Temp_bp));

%% 4. Generate Time-Varying SOC and Temperature Inputs
% Simulation time vector (adjust as needed)
t = (0:1:100)';  % 0 to 100 seconds, 1 sec interval

% Simulated SOC: ramp from 5% to 85%
SOC_signal = linspace(0.05, 0.85, length(t))';

% Simulated Temperature: oscillates between ~29.5 and 32.5
Temp_signal = 31 + 1.5 * sin(0.05 * t);

% Combine time and values for Simulink
SOC_input = [t SOC_signal];
Temp_input = [t Temp_signal];

%% 5. Save All Variables to .mat File for Simulink
save('ECM_ModelData.mat', ...
     'SOC_input', 'Temp_input', ...
     'SOC_bp', 'Temp_bp', ...
     'R0_LUT', 'R1_LUT', 'C1_LUT', 'R2_LUT', 'C2_LUT');
 
 
 
 
 
% code for the ocv lookup table
%% 1. OCV Table Data (from your values)
OCV_table = [3.1610, 3.1961, 3.238, 3.2658, 3.2787, ...
             3.2837, 3.2881, 3.3081, 3.177, 3.4];

SOC_bp_ocv = linspace(0, 1, length(OCV_table));  % 10 SOC breakpoints from 0 to 1

%% 2. Time-varying SOC input signal (simulate SOC over time)
t_ocv = (0:1:99)';  % 100 seconds, 1s interval

% Example: SOC decreasing from 1 to 0 (typical for discharge)
SOC_signal_ocv = linspace(1, 0, length(t_ocv))';

% Format for Simulink From Workspace block
SOC_input_ocv = [t_ocv, SOC_signal_ocv];

%% 3. Save everything to .mat file
save('OCV_LUT_and_Input.mat', ...
     'OCV_table', 'SOC_bp_ocv', 'SOC_input_ocv');

 
 %code for the current input
 %% 1. Define Breakpoints (SOC levels from 0 to 1)
SOC_bp_current = linspace(0, 1, 10);  % 10 points

%% 2. Table Data (Current values at each SOC point)
Current_table = 50 * ones(1, 10);  % All values = 50A

%% 3. Time-Varying SOC Input (to drive the Lookup Table)
t_current = (0:1:99)';  % 0 to 99 seconds, 1-second interval

% Simulated SOC: decreasing linearly from 1 → 0
SOC_signal_current = linspace(1, 0, length(t_current))';
SOC_input_current = [t_current, SOC_signal_current];  % [time, value] format

%% 4. Save All to .mat file
save('Current_LUT_and_Input.mat', ...
     'SOC_input_current', 'SOC_bp_current', 'Current_table');


