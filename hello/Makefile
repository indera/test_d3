help:
	@echo "Available tasks:"
	@echo "\t build/counties.json - convert *.shp file to d3-compatible format"

clean:
	rm build/gz_2010_us_050_00_20m*
	rm build/counties.json
	rm build/states.json
	rm us.json

build/gz_2010_us_050_00_20m.zip:
	mkdir -p $(dir $@)
	curl -o $@ http://www2.census.gov/geo/tiger/GENZ2010/$(notdir $@)


build/gz_2010_us_050_00_20m.shp: build/gz_2010_us_050_00_20m.zip
	unzip -od $(dir $@) $<
	touch $@


build/counties.json_simple: build/gz_2010_us_050_00_20m.shp
	# https://github.com/mbostock/d3/wiki/Geo-Projections#albersUsa
	node_modules/.bin/topojson \
		-o $@ \
		--projection='width = 960, height = 600, d3.geo.albersUsa() \
			.scale(1280) \
			.translate([width / 2, height / 2])' \
		--simplify=.5 \
		--filter=none \
		-- counties=$<


build/counties.json: build/gz_2010_us_050_00_20m.shp build/ACS_12_5YR_B01003_with_ann.csv
	# https://gist.githubusercontent.com/mbostock/9943478/raw/ACS_12_5YR_B01003_with_ann.csv
	node_modules/.bin/topojson \
		-o $@ \
		--id-property='STATE+COUNTY,Id2' \
		--external-properties=build/ACS_12_5YR_B01003_with_ann.csv \
		--properties='name=Geography' \
		--properties='population=+d.properties["Estimate; Total"]' \
		--projection='width = 960, height = 600, d3.geo.albersUsa() \
			.scale(1280) \
			.translate([width / 2, height / 2])' \
		--simplify=.5 \
		--filter=none \
		-- counties=$<

build/states.json: build/counties.json
	# Erase county boundaries ==> we get only state boundaries
	node_modules/.bin/topojson-merge \
		-o $@ \
		--in-object=counties \
		--out-object=states \
		--key='d.id.substring(0, 2)' \
		-- $<


us.json: build/states.json
	node_modules/.bin/topojson-merge \
		-o $@ \
		--in-object=states \
		--out-object=nation \
		-- $<


#  FINANCIAL CHARACTERISTICS FOR HOUSING UNITS WITH A MORTGAGE 2008-2012 American Community Survey 5-Year Estimates
build/counties.json3: build/gz_2010_us_050_00_20m.shp build/ACS_12_5YR_S2506_with_ann.csv
	node_modules/.bin/topojson \
		-o $@ \
		--id-property='STATE+COUNTY,Id2' \
		--external-properties=build/ACS_12_5YR_S2506_with_ann.csv \
		--properties='name=Geography' \
		--properties='value_200k_300k=+d.properties["Owner-occupied housing units with a mortgage; Estimate; VALUE - $200,000 to $299,999"]' \
		--projection='width = 960, height = 600, d3.geo.albersUsa() \
			.scale(1280) \
			.translate([width / 2, height / 2])' \
		--simplify=.5 \
		--filter=none \
		-- counties=$<

