This folder (Code) contains:

- Readme.txt  (this file)	

- data_preprocessing.Rmd
	Used to preprocess large GPS tracks; subsets and interpolates GPS datapoints to filter for
	desired GPS track segments (points above sea, 5 min datapoint resolution, etc.)	
	inputfiles: bird_317.csv
	outputfiles: bird_317_preprocessed.csv

- event_analysis.Rmd
	Used to summarize detected boat event metrics and perform statistical analyses on the data.
	inputfiles: all_boat_events.csv
	outputfiles: event_summary_df.csv

- event_subsetting.Rmd
	Used to extract smaller GPS track segments classified as "boat-following events" based on
	HMM classified behavioural states and movement pattern. Contains additional code for checking
	model recall and precision.	
	inputfiles: bird_317_preprocessed_HMM.csv, event_summary_df.csv, boat_events_hand_picked.xlsx
	outputfiles: all_boat_events.csv

- HMM_model_iterate.Rmd
	Used to run an HMM analysis on GPS tracks. There are 15 iterations of HMM analyses with different input 
	values. From these iteration the model with the best fit is selected and corresponding data is stored.
	inputfiles: bird_317_preprocessed.csv
	outputfiles: bird_317_preprocessed_HMM.csv, best_model_100724.rds

- HMM_optimized.Rmd
	Used to run an HMM analysis on GPS tracks. The best fitted HMM model, selected from the HMM_model_iterate.Rmd
	code is applied to the data. 
	inputfiles: bird_317_preprocessed.csv, best_model_100724.rds
	outputfiles: bird_317_preprocessed_HMM.csv