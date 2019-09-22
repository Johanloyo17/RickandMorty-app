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
                        <!-- barra de navegacion -->
                        <v-toolbar dense >
                            <v-btn  small color="primary"
                                    @click="closeModal()"
                                >
                                <v-icon 
                                    medium
                                    >mdi-chevron-left
                                </v-icon>
                            </v-btn>
                            <v-toolbar-title class="mx-5 title" >Title</v-toolbar-title>
                            <v-spacer></v-spacer>
                            <v-btn icon>
                                <v-icon>mdi-heart</v-icon>
                            </v-btn>
                        </v-toolbar>
                        <!-- imagen portada del modal -->
                        <v-img
                            class="modalFace"
                            src="../assets/fondo-planet.jpg"
                            max-height="200"
                            aspect-ratio="3"
                        >
                            <div class="avatarCont" >
                                <v-avatar
                                    size="150"
                                    color="primary"
                                >
                                    <img :src="characterSelected.image" >
                                </v-avatar>
                                <!-- <v-card-title class="modalName pa-1">character name</v-card-title> -->
                            </div>
                        </v-img>
                    
                    <v-card-actions>
                        <v-tabs
                            v-model="tab"
                            color="primary"
                            grow
                            slider-color="primary"
                        >
                            <!-- tabs burttons -->
                            <v-tab href="#tab1" light nuxt>
                                info
                            </v-tab>
                            <v-tab href="#tab2" light>
                                Episodios
                            </v-tab>
                            <!-- tabs burttons -->
                            
                            <!-- item 1 -->
                            <v-tab-item
                                value="tab1"
                                id="tab1"
                                v-model="tab"
                            >
                                <v-list >
                                    <v-list-item-group
                                        color="primary"
                                    >
                                        <v-list-item 
                                            v-for="(item, index) in info" :key="index"
                                            >
                                            
                                            <v-list-item-content>
                                                <v-list-item-title>{{item}}</v-list-item-title>
                                            </v-list-item-content>
                                        </v-list-item>
                                    </v-list-item-group>
                                </v-list>
                            </v-tab-item>
                            <!-- FIN item 1 -->

                            <!-- item 2 -->
                            <v-tab-item
                                value="tab2"
                                id="tab2"
                                v-model="tab"
                                >   
                                <v-list-item 
                                    v-for="(item, index) in info" :key="index"
                                    >
                                    
                                    <v-list-item-content>
                                        <v-list-item-title>{{item}}</v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-tab-item>
                        </v-tabs><!-- FINtabs burttons -->
                        
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
            mierda: true,
            modalImg:"../assets/modalImg.jpg",
            tab: null,
            infomierda:{
                name: 'johan',
                age: 22,
                lastName: 'Loyo',
            }

        }
    },
    computed: {
        info(){
            if (this.IsModal == false) {
                return console.log("no se ha seleccionado ningun personaje")
            } 
            else{
                return{
                    name : "Nombre:  " + this.characterSelected.name,
                    status :"Estado:  " + this.characterSelected.status,
                    species : "Especie:  " +this.characterSelected.species,
                    gender : "Genero:  " +this.characterSelected.gender,
                    origin : "Origen del personaje:  " +this.characterSelected.origin.name,
                    location : "Localizacion del personje:  " +this.characterSelected.location.name,
                }
            }
        }
    },
    created () {
        let modalImg = "../assets/modalImg.jpg"
        
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
        min-height 90vh !important
    .avatarCont
        display flex 
        flex-direction column
        justify-content center
        align-items center
        height: 100%
        .modalName
            color white
            font-weight bold
</style>