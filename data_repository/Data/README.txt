This folder (Data) contains:

- Readme.txt  (this file)

- best_model_100724.rds
	Rdata containing data and variables of best fitted HMM model from 15 iterations.
	Data was created using HMM_model_iterate.Rmd.

- bird_317.csv
	GPS-track data of Lesser Black-backed Gull with tracker ID 317.
	Dataset was downloaded from https://www.uva-bits.nl/virtual-lab/.
	
	Datafile contains 23 variables of which 4 were mainly used during this project. Only used variables
	and their metrics are described here. 
	For data explanation on the other variables please refer to https://www.uva-bits.nl/virtual-lab/.
	
	Variable, data_type, range, unit, definition
	"device_info_serial", num, [317], int, serial number of tracking device
	"date_time", POSIXct, [2015-01-04 15:51:45, 2017-07-28 09:34:57], YYYY-MM-DD HH:MM:SS, date and time stamp of when GPS datapoint was collected
	"latitude", num, [36.67, 53.21], latitude, latitude of measurement point
	"longitude", num, [-6.462733, 5.696396], longitiude, longitude of measurement point

- bird_317_preprocessed.csv
	Preprocessed GPS-track data of Lesser Black-backed Gull with tracker ID 317.
	Dataset was created using data_preprocessing.Rmd script with "bird_317.csv" as input.  
	
	Datafile is largely similar to "bird_317.csv", but with 8 added variables. Only added variables
	and their metrics are described here.
	
	Variable, data_type, range, unit, definition
	"UTMzone", num, [30:31], int, UTM zone corresponding to longitude and latitude of GPS datapoint
	"x", num, [269432, 731589], UTME, UTME coordinate of GPS datapoint
	"y", num, [4059448, 5896755], UTMN, UTMN coordinate of GPS datapoint
	"sea_indicator", logical, [TRUE, FALSE], x, logical operator indicating whether GPS datapoint was measured above sea
	"index", num, [3377, 46429], int, rowindex used to indicate consecutive GPS datapoints
	"track_id", num, [1, 452], int, ID used to cluster consecutive GPS datapoints into tracks
	"dt", num, [1198, 46838], seconds, difference in timestamp between current and previous GPS datapoint
	"time_seconds", num, [1.426e+09, 1.501e+09], seconds, "date_time" variable converted into seconds

- bird_317_preprocessed_HMM.csv
	HMM analysed preprocessed GPS-track data of Lesser Black-backed Gull with tracker ID 317.
	Dataset was created using HMM_optimized.Rmd script with "bird_317_preprocessed.csv" as input.  
	
	Datafile is largely similar to "bird_317_preprocessed.csv", but with 1 added variable. Only added variables
	and their metrics are described here.
	
	Variable, data_type, range, unit, definition
	"States", chr, ["Transit", "ARS", "Exploratory Flight", "Float", "Shrimp boat", "Stationary", "Trawler"], 
		x, predicted state ascribed to GPS datapoint by Hidden Markov model analysis

- boat_events_hand_picked.xlsx
	Data collected on hand picked GPS track segments expected to signal a "boat following event". Data
	was used to check analysis pipeline accuracy.

	Datafile contains 8 variables.

	Variable, data_type, range, unit, definition
	"Event nr.", num, [1, 50], int, index indicating the event ID
	"Bird ID", num, [5460263, 5557897], int, ID of tagged Lesser Black-backed Gull
	"Device ID", num, [534, 7086], int, serial number of tracking device
	"Start time", POSIXct, [10-6-2016  16:59:02, 25-7-2022  08:16:08], YYYY-MM-DD HH:MM:SS, date and time stamp of when event started 
	"End time", POSIXct, [10-6-2016  21:27:50, 25-7-2022  16:04:34], YYYY-MM-DD HH:MM:SS, date and time stamp of when event ended
	"Male/Female", chr, ["M", "F"], x, sex of Lesser Black-backed Gull
	"Event type", chr, ["Shrimp trawler", "Trawler"], x, classification (based on average travel speed) of event type
	"Notes", chr, [various], x, notes on selected event

- event_summary_df.csv
	Summary dataset with information all detected boat-following events. 
	Dataset was created using event_subsetting.Rmd and event_analysis scripts with "bird_317_preprocessed_HMM.csv" as input.

	Datafile contains 19 variables.

	Variable, data_type, range, unit, definition
	"device", num, [317, 7068], int, serial number of tracking device
	"event_id", num, [5, 4025], int, index indicating the event ID
	"start_time", POSIXct, [2015-02-07 11:25:38, 2022-11-05 19:41:40], YYYY-MM-DD HH:MM:SS, date and time stamp of when event started
	"end_time", POSIXct, [2015-02-07 17:49:24, 2022-11-06 01:35:43], YYYY-MM-DD HH:MM:SS, date and time stamp of when event ended 
	"event_duration", num, [28.82, 1220.95], mins, duration of the detected event in minutes
	"year", num, [2015, 2022], year, year in which the event was detected
	"month", chr, ["Jan", "Dec"], month, month in which the event was detected
	"weekday", chr, ["Mon", "Sun"], day, day of the week on which the event was detected
	"center_x", num, [224532, 763502], longitude, longitude coordinate of centre point of event
	"center_y", num, [2037426, 5971871], latitude, latitude coordinate of centre point of event
	"event_type", chr, ["Trawler", "Shrimp boat"], event type, type of event as classified by HMM states
	"UTMzone", num, [28, 32], int, UTM zone corresponding to longitude and latitude of event centre 
	"longitude", num, [-17.644, 10.284], longitude, longitude of event centre
	"latitude", num, [18.42, 53.89], latitude, latitude of event centre
	"distance_to_colony", num, [5.471, 4269.333], km, distance of event centre to colony centre on Texel
	"sex", chr, ["M", "F"], x, sex of Lesser Black-backed Gull
	"effort", num, [125760, 529679], int, effort determined by number of datapoints per year (used for statistics)
	"n_events", num, [15, 92], int, number of events detected in corresponding year (used for statistics)
	"grouped_days", chr, ["weekend_days", "fishing_days"], day type, event detection day classified as one of the two day groups