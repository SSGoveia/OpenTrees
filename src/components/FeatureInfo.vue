<template lang="pug">
div
    div(v-if="feature")
        //- img.image(v-if="imageUrl" :src="imageUrl")
        h2.i.lancelot.f3.bg-green.pa2.mv0 {{ p.common || p.scientific }}
        div(v-if="p.class").f7.pa2.i
            | {{ p.class }} 
            span.light-green > 
            | {{ p.subclass }} 
            span.light-green > 
            | {{ p.family }}
            
        table#FeatureInfo(v-if="feature").bg-white.helvetica.ma1
            tr(v-if="p.scientific")
                th Scientific name
                td {{ p.scientific }}
            tr(v-if="p.common")
                th Common name
                td {{ p.common }}
            tr(v-if="p.variety")
                th Variety
                td {{ p.variety }}
            tr(v-if="p.dbh")
                th Diameter
                td {{ p.dbh }} 
                    span.detail cm.
            tr(v-if="p.height")
                th Height
                td {{ p.height }} 
                    span.detail m.
            tr(v-if="p.planted")
                th Planted
                td {{ p.planted }}
            tr(v-if="p.maturity")
                th Maturity
                td {{ p.maturity }}
            //- tr(v-if="p.")
            //-     th 
            //-     td {{ p }}
            tr(v-if="p.species_count")
                th Count
                td {{ p.species_count.toLocaleString() }} 
                    span.detail similar trees
            tr(v-if="p.ref")
                th ID
                td {{ `#${p.ref}` }}
                
            //- tr(v-for="(value, prop) in p")
            
            //-     template(v-if="ignoreProps.indexOf(prop) === -1")
            //-         th.f6.dark-green {{ prop }}
            //-         td.f6 {{ value }}
        p.f7.tr.gray.mh2.i Source: {{ p.source }}
        Wikipedia(:searchTerm="p.scientific")
    div(v-else) Click on a tree for information!
</template>

<script>
import Wikipedia from './Wikipedia';
export default {
    name: "FeatureInfo",
    data: () => ({
        feature: undefined,
        ignoreProps: ['id','Longitude','Latitude', 'image_url']
    }),
    components: { Wikipedia },
    computed: {
        p() {
            return this.feature && this.feature.properties || {};
        },
        imageUrl() {
            return this.p && this.p.image_url
        },
    },
    created() {
        window.app.FeatureInfo = this;
    }
}
</script>

<style scoped>
#FeatureInfo th {
    text-align:  right;
}

.image {
    width: 100%;
}
</style>
<style>
.bg-green {
    background: hsl(98.6, 30.4%, 82%) !important;
}

.dark-green {
    color: hsl(100, 29.4%, 30%) !important;
}

.light-green {
    color: hsl(100, 29.4%, 50%) !important;
}

.lancelot {
    font-family:lancelot,sans-serif;
}
th {
    color: hsl(100, 29.4%, 30%)
}
td {
    padding-left:8px;
}
.detail {
    /* color:#444; */
    font-weight:200;
    font-size:75%;
}
</style>