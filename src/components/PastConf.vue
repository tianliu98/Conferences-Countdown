<template>
    <div class="conf">
        <div id="item-content">
            <div id="item-col">
                <h2><a v-bind:href='url'>{{ name }}</a></h2> 
                <p>Location: {{ location }}</p>
            </div>

            <div id="item-col">
                <h2>Past Due</h2>
                <p>Deadline: {{ deadline }}</p>
            </div>
        </div>
        
        <div class="ui divider"></div>
    </div>
</template>


<script>
export default {
    name: 'PastConf',
    props: ['name', 'deadline', 'location', 'url'],
    data() {
        return {
            DD: 0,
            HH: 0,
            MM: 0,
            SS: 0,
            is_expired: false
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