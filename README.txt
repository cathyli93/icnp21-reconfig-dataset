###############################################################################
#   Rperf Dataset Release (ICNP'21)
#
###############################################################################

We introduce released datasets by our ICNP'21 work: “Reconfiguring Cell Selection in 4G/5G Networks”.

We conducted measurement study in Los Angeles (CA) with AT&T and T-Mobile. We run our experiments through MI-LAB testbed (http://milab.cs.purdue.edu/).

In particular, we run two distinct types of experiments for to build profile for cells:

(I) Network downlink speed test while driving to scan all roads in a selected region at LA. At the same time, let the mobile devices run heavy traffic flows (here, continuously downloading files from the lab server).

(II) Network cell deployement and signal strength measurements. We drove along all roads in the same region, and let mobile devices run light traffic flows (Ping Google every second).

Both type-I static and type-I driving experiments are performed via the mperf task in MI-LAB and was primarily performed from Apr to Aug 2021.

We have two datasets collected at the same region, over AT&T and T-Mobile; Each dataset contains both type-I and type-II data.
1. C1_att - Data collection for AT&T.
2. C1_tmobile - Data collection for T-Mobile


1) Structure of files

├── dataset_C1_att
│   ├── data_310410.csv
│   ├── handoffs.csv
│   ├── radio_measurement
│   │   ├── rss_data_2021*.csv
│   │   ├── ....
├── dataset_C1_tmobile
│   ├── data_310260.csv
│   ├── handoffs.csv
│   ├── radio_measurement
│   │   ├── rss_data_2021*.csv
│   │   ├── ....

2) Data File Descriptions (*.csv)

-------------------------------------------------------------------------------
Data speed samples of serving cell sets: data_310410.csv/data_310260.csv
-------------------------------------------------------------------------------

This is the data collection for heavy downloading test. We record its serving cells set and instant throughput (per second).

Data file format:
grid_lat:                           latitude of grid (precision 0.0005)
grid_lon:                           longitude of grid (precision 0.0005)
pcell_cid:                          physical cell ID of PCell
pcell_freq:                         downlink earfcn of PCell
scell_1_cid:                        physical cell ID of SCell1
scell_1_freq:                       downlink earfcn of SCell1
scell_2_cid:                        physical cell ID of SCell2
scell_2_freq:                       downlink earfcn of SCell2
scell_3_cid:                        physical cell ID of SCell3
scell_3_freq:                       downlink earfcn of SCell3
nr_cid:								physical cell ID of the NR cell
nr_freq:							downlink arfcn of the NR cell
seconds_since_epoch:                datetime in epoch format
throughput:                         bits per secound
past_seconds_since_rrc_request:     past seconds since device receives an RRC
                                    request

-------------------------------------------------------------------------------
Radio signal strength samples of all serving cells and neighbor cells: 
radio_measurement/rss_data_*.csv
-------------------------------------------------------------------------------

This is the data collection to learn the cell signal strength in the drive tests. It runs a mice flow (keeps pinging Google), rather than the heavy file downloading to save the data usage. We record all measurement logs of RSRP/RSRQ of serving/neighbor cells.

Data file format:
lat:			latitude
lon:			longitude
timestamp:		datetime in epoch format
freq:			downlink earfcn of measured cell
cid:			physical cell ID of measured cell
rsrp:			RSRP (in dBm) of measured cell
rsrq:			RSRQ (in dB) of measured cell	
type:			type of measured cell - PCell/SCell/neighbor cell	

-------------------------------------------------------------------------------
Handoff instances: handoffs.csv
-------------------------------------------------------------------------------

This is the collection of all handoffs collected during heavy downloading tests.

Data file format:
time:				datetime in epoch format
lat:				latitude
lon:				longitude
servingFreq:		downlink earfcn of source PCell
servingCid:			physical cell ID of source PCell
targetFreq:			downlink earfcn of target PCell
targetCid:			physical cell ID of target PCell
1_SCell_freq:		downlink earfcn of SCell1 after handoff
1_SCell_cid:		physical cell ID of SCell1 after handoff
2_SCell_freq:		downlink earfcn of SCell2 after handoff
2_SCell_cid:		physical cell ID of SCell2 after handoff
3_SCell_freq:		downlink earfcn of SCell3 after handoff
3_SCell_cid:		physical cell ID of SCell2 after handoff
NR_freq:			downlink earfcn of serving NR cell after handoff
NR_cid:				physical cell ID of serving NR cell after handoff
config:				configuration of source PCell
	Tuple format:
	earfcn of measured frequency channel,
	measurement ID,
	measurement event type (e.g. a2/a3),
	time to trigger report,
	quantity to trigger report,
	allowed counts of reports,
	the 1st parameter for the measurement event (or report triggering condition),
	(optional) the 2nd parameter for the measurement event (or report triggering condition)
reports:			received reports before handoff
	Tuple format:
	datetime
	physical cell ID of reported cell
	RSRQ of serving PCell
	RSRP of serving PCell
	RSRQ of reported cell
	RSRP of reported cell
