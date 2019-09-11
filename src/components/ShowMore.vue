<template>
    <div>
                        <!-- <v-btn icon dark @click="closeModal()">
                            <v-icon>mdi-close</v-icon>
                        </v-btn> -->
        <v-overlay :value="Isloading">
            <v-progress-circular indeterminate size="64" color="primary"></v-progress-circular>
        </v-overlay>

        <v-row justify="center">
            <v-dialog  v-model="IsModal" persistent min-width="300" width="600">
                <v-card class="modalCharacter">
                    <v-card-title class="headline">Use Google's location service?</v-card-title>
                    <v-card-text>Let Google help apps determine location. This means sending anonymous location data to Google, even when no apps are running.</v-card-text>
                    <v-card-actions>
                        <div class="flex-grow-1"></div>
                        <v-btn color="green darken-1" text @click="dialog = false">Disagree</v-btn>
                        <v-btn color="green darken-1" text @click="dialog = false">Agree</v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-row>
    </div>
</template>

<script>
export default {
    props: [
        "characterSelected",
        "IsModal",
        'Isloading'
    ],
    data() {
        return {
        
        }
    },
    methods:{
        closeModal(){
            console.log("cerrando modal!")
            this.$emit('closeModal')
        }
    }
    
};
</script>
<style lang="stylus">
    .modalCharacter
        height 90vh !important
</style>