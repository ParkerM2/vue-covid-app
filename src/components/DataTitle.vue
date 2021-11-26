<template>
    <div class="text-center">
    <h2 class="text-3x1 font-bold">{{ text }}</h2>
    <div class="text-2x1 mt-4 mb-10">
        {{timestamp}}
    </div>
    </div>
</template>

<script>
    // import { ref } from 'vue';
    import dayjs from 'dayjs';
    import {computed } from 'vue';
    
    export default {
        name: 'DataTitle',
        props: ['text', 'dataDate'],
        
        setup () {
            return {
                timestamp: dayjs().format('MMMM D YYYY, h:mm:ss a')
        }    
    }
    }
</script>