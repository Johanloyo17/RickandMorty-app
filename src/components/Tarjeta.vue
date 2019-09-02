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
            <span>Number 10</span><br>
            <span class="text--primary">
                <span>Whitehaven Beach</span><br>
            </span>
        </v-card-text>

        <!-- buttons -->
        <v-card-actions>
            <v-btn
                text
                color="orange"
            >
                Share
            </v-btn>
            <v-btn
                text
                color="orange"
            >
                Explore
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
}
</script>