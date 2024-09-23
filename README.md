# 2DF20---Assignment-2
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt
import geopandas as gpd
dataOrg = pd.read_csv('earthquake_dataset.csv')

filtered_data_higher = dataOrg[dataOrg['mag'] >= 5]
filtered_data_lower = dataOrg[dataOrg['mag'] < 5]

result_higher = filtered_data_higher[['mag']]
result_lower = filtered_data_lower[['mag']]

count_higher = filtered_data_higher['mag'].count()
count_lower = filtered_data_lower['mag'].count()

print(result_higher)
print("Number of values with mag >= 5:", count_higher)

print(result_lower)
print("Number of values with mag < 5:", count_lower)


# Plot map of investigating region
df_geo = gpd.GeoDataFrame(dataOrg, geometry = gpd.points_from_xy(dataOrg.longitude, dataOrg.latitude))
print(df_geo)
world_data = gpd.datasets.get_path('naturalearth_lowres')

# Example tepmplate from assignment file
dataOrg['DateTime'] = pd.to_datetime(dataOrg['time'])
data = dataOrg.sort_values(by='DateTime')
selection1 = (data['DateTime'].dt.year >= 1980) & (data['DateTime'].dt.year < 2010)
selection2 = data['place'].str.contains('netherlands', case=False)
data = data[selection1 & selection2]
