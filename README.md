# Data description

The following files contain the two networks, and a corresponding municipality map which are used in the manuscript Menyhért, M., Bokányi, E., Corten, R., Heemskerk, E. M., Kazmina, Y., & Takes, F. W. (2024). Connectivity and Community Structure of Online and Register-based Social Networks. arXiv preprint arXiv:2406.17752., https://arxiv.org/abs/2406.17752.

One network is the municipality-level aggregation of the Dutch online social network (OSN) Hyves, represending online friendship connections between users of the platform.

The other network is the municipality-level aggregation of the register-based social network (RSN) of the Netherlands as of 2010, using family, school, and work connections of Statistics Netherlands. We refer to the different types of connections as layers of the network, and give the aggregation for all layers, and for each of the layers separately.

## Nodes

Nodes are the 431 municipalities of the Netherlands as of 2010. The following links contain helpful resources to obtain additional metadata or the map of the munacipality boundaries:
* https://www.cbs.nl/nl-nl/dossier/nederland-regionaal/geografische-data/wijk-en-buurtkaart-2010
* https://www.cbs.nl/nl-nl/nieuws/2010/01/herziene-versie-431-gemeenten-in-2010
* https://www.cbs.nl/nl-nl/cijfers/detail/80397ned
* https://www.cbs.nl/nl-nl/onze-diensten/methoden/classificaties/overig/gemeentelijke-indelingen-per-jaar/indeling-per-jaar/gemeentelijke-indeling-op-1-januari-2010

`nodes.csv`:
* `label` : municipality code, can be matched with other official statistics
* `municipality_name` : municipality name
* `lat` : latitude of centroid
* `lon` : longitude of centroid
* `osn_user_count` : number of users in the Hyves network in the municipality
* `rsn_population` : number of people in the Statistics Netherlands network in the municipality
* `location_x` : centroid x coordinate of municipality in the Amersfoort coordinate system (https://epsg.io/28992)
* `location_y` : centroid y coordinate of municipality in the Amersfoort coordinate system (https://epsg.io/28992)


## Edges

Edges contain how many connections go between users / people of a given municipality pair. Self-edges, e.g. where the source and target municipalities are the same are included. In this case, it should be taken into account that the counts count every connection twice: once from each user / people endpoint. The network is undirected, thus each municipality pair is listed once.

Because of disclosure risk, any municipality pair  is omitted for which any of the counts, e.g. Hyves connection count, Statistics Netherlands network all layers, family layer, work layer, or school layer is smaller than 10.

`edges.csv`:
* `source_label` : municipality code of the alphabetically smaller municipality from the pair
* `target_label` : municipality code of the alphabetically larger municipality from the pair
* `osn_user_count` : number of connections between users of the Hyves network between the two municipalities
* `rns_all_layers_count` : number of connections of any type between people living in the two municipalities (for self-loops, this should be divided by 2)
* `rns_family_count` : number of family connections between people living in the two municipalities (for self-loops, this should be divided by 2)
* `rns_school_count` : number of family connections between people living in the two municipalities (for self-loops, this should be divided by 2)
* `rns_work_count` : number of family connections between people living in the two municipalities (for self-loops, this should be divided by 2)
* `distance` : distance between municipality centroids in meters, measured from `location_x`, `location_y` in `nodes.csv`

##  Map

`gem_2010_v3.shp` and additional helper files contain the official municipality shapefile downloaded from the website of Statistics Netherlands as of 23-09-2024.
