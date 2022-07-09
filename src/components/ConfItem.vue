<template>
    <div class="conf">
        <div id="item-content">
            <div id="item-col">
                <h2><a v-bind:href="url">{{ name }}</a></h2> 
                <p>Location: {{ location }}</p>
            </div>

            <div id="item-col">
                <h2 v-if="is_expired == false">{{DD}}days {{HH}}h {{MM}}m {{SS}}s</h2>
                <h2 v-else>Past Due</h2>
                <p>Deadline: {{ deadline }}</p>
            </div>
        </div>
        
        <div class="ui divider"></div>
    </div>
</template>


<script>
export default {
    name: 'ConfItem',
    props: ['name', 'deadline', 'location', 'url'],
    data() {
        return {
            DD: 0,
            HH: 0,
            MM: 0,
            SS: 0,
            is_expired: false,
        }
    },
    mounted() {
        this.countdown()
        setInterval( this.countdown, 1000)
    },
    methods: {
        countdown: function(){
            var countDownDate = new Date(this.deadline).getTime()
            var now = new Date().getTime();
            var distance = countDownDate - now;
            this.DD = Math.floor(distance / (1000 * 60 * 60 * 24));
            this.HH = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            this.MM = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            this.SS = Math.floor((distance % (1000 * 60)) / 1000);
            if (distance < 0){
                this.is_expired = true
                location.reload()
            }
        }
    }
}
</script>


<style scoped>
.conf {
    padding-top: 20px;
}

#item-col {
    float: left;
    width: 50%;
}

#item-content:after {
  content: "";
  display: table;
  clear: both;
}

a:link {
    color: black;
    text-decoration: underline;
}

a:visited {
    color: black;
    text-decoration: underline;
}

a:hover {
    color: darkgray;
    text-decoration: underline;
}

a:active {
    color: black;
    text-decoration: underline;
}

</style>