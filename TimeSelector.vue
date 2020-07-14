<template>
	<timeselector :value="getDate" v-model="date" displayFormat="HH:mm" v-on:input="emitTime" returnFormat="hh:mm" class="form-control text-center input-1" :placeholder="'--:-- -'"></timeselector>
</template>

<script>
    import moment from 'moment-timezone'
    Vue.use(require('vue-moment'), {
        moment,
    });

    import TimeSelector from 'vue-timeselector';

    export default {
        name: 'TimeSelector',
        components: {
            timesector: TimeSelector,
        },
        data: function() {
            return {
                date: '',
            }
        },
        computed: {
            getDate() {
                if (this.date && moment(this.date).isValid()) {
                    this.date = moment(this.date).tz('America/Santiago').format('HH:mm');
                }
                return this.date;
            },
        },
        methods: {
            emitTime: function(e) {
                this.$emit('input', moment(this.from).format('YYYY-MM-DD')+' a '+moment(this.to).format('YYYY-MM-DD'));
            },
            limpiar: function () {
                this.date = null;
            }
        },
    }
</script>