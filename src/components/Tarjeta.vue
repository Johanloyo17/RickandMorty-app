<template>
    <v-card
        class="mx-auto"
    >
        <!-- head -->
        <v-img
            class="white--text"
            height="200px"
            :src="item.image"
        >
            <v-card-title class="align-end fill-height">{{item.name}}</v-card-title>
        </v-img>

        <!-- cont -->
        <v-card-text>
            <span>{{item.origin.name}}</span><br>
            <span class="text--primary">
                <span>{{item.species}}</span><br>
            </span>
        </v-card-text>

        <!-- buttons -->
        <v-card-actions>
            <v-btn
                text
                color="orange"
                @click="showMore(item.id)"
            >
                Ver mas 
            </v-btn>
            
        </v-card-actions>
    </v-card>

</template>
<script>
export default {
    props: ['item'],
    data() {
        return {
            
        }

    },
    methods:{
        showMore(id){
            this.$emit('showModal', id)
            
        } 
    }

}
</script>