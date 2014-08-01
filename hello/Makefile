help:
	@echo "Available tasks:"
	@echo "\t build/counties.json - convert *.shp file to d3-compatible format"\t"

build/gz_2010_us_050_00_20m.zip:
	mkdir -p $(dir $@)
	curl -o $@ http://www2.census.gov/geo/tiger/GENZ2010/$(notdir $@)


build/gz_2010_us_050_00_20m.shp: build/gz_2010_us_050_00_20m.zip
	unzip -od $(dir $@) $<
	touch $@


build/counties.json: build/gz_2010_us_050_00_20m.shp
	# https://github.com/mbostock/d3/wiki/Geo-Projections#albersUsa
	node_modules/.bin/topojson \
		-o $@ \
		--projection='width = 960, height = 600, d3.geo.albersUsa() \
			.scale(1280) \
			.translate([width / 2, height / 2])' \
		--simplify=.5 \
		--filter=none \
		-- counties=$<
