<template>
    <div>
    <span class="clock-display">{{time}}</span>
    </div>
</template>

<script>
function zeroPadding(num, digit) {
    var zero = '';
    for(var i = 0; i < digit; i++) {
        zero += '0';
    }
    return (zero + num).slice(-digit);
}

export default {
    data() {
        return {
            time: "",
        };
    },
    mounted() {
       
        var timerID = setInterval(this.updateTime, 1000);
        this.updateTime();

    },
    methods: {
        updateTime() {
             var week = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'];
            var cd = new Date();
            this.time = zeroPadding(cd.getHours(), 2) + ':' + zeroPadding(cd.getMinutes(), 2) + ':' + zeroPadding(cd.getSeconds(), 2) + " - " + zeroPadding(cd.getFullYear(), 4) + '-' + zeroPadding(cd.getMonth()+1, 2) + '-' + zeroPadding(cd.getDate(), 2) + ' ' + week[cd.getDay()];

        }
    }
}
</script>

<style lang="scss" scoped>

</style>