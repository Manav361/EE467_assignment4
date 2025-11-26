# Team Members
1) Manav Agrawal
2) Aviral Goel
3) Aagam Shah
4) Akshat Singhvi



# Time Feature Engineering - Summary

## Changes Made to AC_analysis_and_models.ipynb

### 1. **Time Feature Extraction (New Section 6)**
   - **Created time_only column**: Extracts the time component from timestamp (HH:MM:SS format)
   - **Created seconds_since_midnight column**: Converts the timestamp to seconds elapsed since midnight (0-86399 seconds)
   - This consolidates hour, minute, and second information into a single continuous feature

### 2. **Features Added to Feature Engineering**
   - `time_only`: Time component of timestamp
   - `seconds_since_midnight`: Continuous time feature (seconds from midnight)
   - `second`: Second component (0-59)
   
   These join existing time features:
   - `hour`: Hour of day (0-23)
   - `minute`: Minute of hour (0-59)
   - `day_of_week`: Day of week (0-6, Monday-Sunday)

### 3. **Updated Classification Features**
   - Added 15 total features including the new time-based features:
     ```python
     classification_features = [
         'AC_activepower', 'AC_reactivepower', 'hour', 'day_of_week', 'minute', 'second',
         'apparent_power', 'power_factor', 'reactive_to_active_ratio',
         'activepower_lag1', 'activepower_lag2', 'reactivepower_lag1',
         'activepower_rolling_mean_5', 'reactivepower_rolling_mean_5', 
         'seconds_since_midnight'
     ]
     ```

### 4. **Time Feature Visualization**
   - **Distribution of Time Feature**: Shows seconds_since_midnight is uniformly distributed across 24-hour period
   - **Average AC Power by Hour**: Peak power at 17:00 (544W), lowest at 05:00 (84W)
   - **AC ON Percentage by Hour**: AC is most active 17:00-20:00 (>80% ON), least active 04:00-07:00 (<15% ON)
   - **Power vs Time of Day**: Clear temporal patterns show AC usage peaks in evening hours

### 5. **Key Insights from Time Feature**
   - **Highest power consumption hour**: 17:00 (5:00 PM) - 544W average
   - **Lowest power consumption hour**: 05:00 (5:00 AM) - 84W average
   - **Peak AC usage period**: 17:00-20:00 (6.64x higher ON rate than early morning)
   - **Strong temporal dependency**: AC status is highly dependent on time of day

### 6. **Benefits of Time Features**
   - **seconds_since_midnight**: Single continuous feature capturing time-of-day patterns
   - **Combination with other features**: hour, minute, second allow fine-grained temporal analysis
   - **Improved model interpretability**: Easy to understand time-dependent AC behavior
   - **Better predictions**: Models can learn strong temporal patterns (cooling/heating peaks)

## Dataset Statistics
- **Total samples**: 165,493 (after removing NaN from feature engineering)
- **Date range**: 2025-10-12 to 2025-10-29 (18 days)
- **AC Status**: 59.8% OFF, 40.2% ON
- **Seconds_since_midnight range**: 0 to 86,399 (full 24-hour cycle)

## Model Training Impact
The inclusion of time features provides models with:
1. Temporal patterns (peak vs off-peak hours)
2. Hourly variations in power consumption
3. Daily cyclical patterns
4. Better classification of AC on/off status
5. More accurate power prediction based on time of day
