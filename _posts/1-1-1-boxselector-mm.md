---
title: Box Selector
tags: ModestMaps
layout: control
---

A control that enables users to select a bounds on a map by holding the shift
key and dragging on a map. It's useful for stuff like selecting areas to
render in [TileMill](http://mapbox.com/tilemill) or areas to download for
offline use.

{% highlight html %}
<script>
var tilejson = {
  tilejson: '1.0.0',
  scheme: 'tms',
  tiles: ['http://a.tiles.mapbox.com/mapbox/1.0.0/blue-marble-topo-bathy-jul/{z}/{x}/{y}.png']
};
var mm = com.modestmaps;
var m = new mm.Map('modestmaps-boxselector',
  new wax.mm.connector(tilejson),
  new mm.Point(240,120));
wax.mm.boxselector(m, tilejson, {
  callback: function(coords) {
    $('#boxselector-text').text(
      coords.map(function(c) {
        return c.lat + ',' + c.lon;
      }).join(' - '));
  }
});
m.setCenterZoom(new mm.Location(39, -98), 2);
</script>
<div class='widget'>Selection: <span id='boxselector-text'></span></div>
</div>


{% endhighlight %}

## API

<dl>
  <dt>{% highlight js %}var boxselector = wax.mm.boxselector(map, options or callback){% endhighlight %}</dt>
  <dd>Create a new boxselector object. The second argument can be either an
  options object with a 'callback' member for a callback function, or just
  a callback function. Options is an object with options:
  <dl>
    <dt>callback</dt>
    <dd>A function that will be called with a single argument
    <code>coords</coords>, containing the extent of a selection, as represented
    by an array with two elements of type com.modestmaps.Location.
    </dd>
  </dl>
</dl>