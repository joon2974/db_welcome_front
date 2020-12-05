<template>
    <v-card
        class="mx-auto mt-5 ml-8"
        max-width="600"
        width="400">
        <v-img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTbrICLaODtIo6d3yqnZIbmLfZfNffUPhEsag&usqp=CAU"
            height="200px">
        </v-img>

        <v-card-title>
            {{spaceCardInfo.name}}
        </v-card-title>

        <v-card-subtitle>
            {{spaceCardInfo.region}} | {{spaceCardInfo.exclusiveArea}}/{{spaceCardInfo.publicArea}} | {{spaceCardInfo.rentCost}}
             | {{spaceCardInfo.spaceType}} | {{spaceCardInfo.vacantRoomCount}} | 가성비 점수 {{spaceCardInfo.score}}점! 
        </v-card-subtitle>

        <v-card-actions>
            <v-dialog
                v-model="show"
                persistent
                max-width="300">
                <template v-slot:activator="{on, attrs}">
                    <v-btn
                        color="orange lighten-2"
                        text
                        v-bind="attrs"
                        v-on="on"
                        >
                        추가정보
                    </v-btn>
                </template>
                <v-card>
                    <v-card-title>
                        {{spaceCardInfo.name}} 상세정보
                    </v-card-title>
                    <v-card-subtitle>
                        {{spaceCardInfo.region}} | {{spaceCardInfo.exclusiveArea}}/{{spaceCardInfo.publicArea}} | {{spaceCardInfo.rentCost}}
                        | {{spaceCardInfo.spaceType}} | {{spaceCardInfo.vacantRoomCount}} | 가성비 점수 {{spaceCardInfo.score}}점!
                    </v-card-subtitle>
                    <v-card-subtitle>
                        연락처: {{spaceCardInfo.contactNum}}
                    </v-card-subtitle>
                    <v-card-subtitle>
                        홈페이지: {{spaceCardInfo.homepageUrl}}
                    </v-card-subtitle>
                    <v-card-actions>
                        <v-btn
                            color="green darken-1"
                            text
                            @click="switchShow">
                            확인
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    props: ["spaceCardInfo"],

    data: () => ({
        show: false
    }),

    methods: {
        switchShow() {
            this.show = !this.show;
        }
    }
}
</script>