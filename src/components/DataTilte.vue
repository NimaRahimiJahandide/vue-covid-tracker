
import { text } from 'node:stream/consumers';


import { text } from 'stream/consumers';


import { text } from 'express';


import { text } from 'body-parser';


import { text } from 'body-parser';

<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{ text }}</h2>
        <div class="text-2xl mt-4 mb-10">
            {{ timestamp }}
        </div>
    </div>
</template>

<script>
import moment from 'moment';

export default{
    name: 'DataTitle',
    props: ['text', 'dataDate'],
    computed: {
        timestamp: function(){
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
        }
    }
}
</script>