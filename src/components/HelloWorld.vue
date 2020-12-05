<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="3">
        <h1 class="mb-2">
          필터 설정
        </h1>
        <v-divider></v-divider>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>선호지역</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0 mt-2"
            style="height: 70px">
            <v-select
              flat
              v-model="region"
              :items="regionItems"
              label="지역 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>공용면적</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0"
            style="height: 70px">
            <v-select
              flat
              v-model="publicArea"
              :items="publicAreaItems"
              label="공용면적 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>전용면적</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0"
            style="height: 70px">
            <v-select
              flat
              v-model="exclusiveArea"
              :items="exclusiveAreaItems"
              label="전용면적 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>임대금액</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0"
            style="height: 70px">
            <v-select
              flat
              v-model="rentCost"
              :items="rentCostItems"
              label="임대금액 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>공간유형</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0"
            style="height: 70px">
            <v-select
              flat
              v-model="spaceType"
              :items="spaceTypeItems"
              label="공간유형 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col 
            cols="5" 
            class="d-flex align-center justify-center pa-0"
            style="height: 70px">
            <h2>공실개수</h2>
          </v-col>
          <v-col 
            cols="7"
            class="pa-0"
            style="height: 70px">
            <v-select
              flat
              v-model="vacantRoom"
              :items="vacantRoomCountItems"
              label="공실개수 선택">
            </v-select>
          </v-col>
        </v-row>
        <v-btn
          tile
          color="primary"
          class="mt-2"
          @click="search">
          검색
        </v-btn>
      </v-col>

      <v-col cols="9">
        <h1 class="display-2 font-weight-bold mb-3">
          검색 목록
        </h1>
        <v-divider></v-divider>
        <v-skeleton-loader
          v-if="filterOptions.region.length === 0"
          v-bind="filterOptions"
          type="list-item-avatar, divider, list-item-two-line, card-heading, image, actions"
          class="mt-4 ml-4">
        </v-skeleton-loader>
        <v-row
          v-else>
          <space-card 
            v-for="spaceInfo in spaceInfos" 
            :key="spaceInfo.name"
            :spaceCardInfo="spaceInfo">
          </space-card>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
import SpaceCard from './SpaceCard.vue';

const headers = {
  "Content-type": "application/json; charset=UTF-8",
  Accept: "/*",
  "Access-Control-Allow-Origin": "*"
};

  export default {
    name: 'HelloWorld',

    components: {'space-card': SpaceCard},

    created() {
      // 디폴트값 불러오기
      console.log(this.filterOptions.region.length);
    },

    data: () => ({
      filterOptions: {
        region: "",
        exclusiveArea: "",
        publicArea: "",
        rentCost: "",
        spaceType: "",
        vacantRoomCount: ""
      },
      regionItems: [
        "서울", "부산", "울산", "대구", "경북", "광주", "전남", "제주", "인천", "대전", "충남", "세종", "강원", "충북", "전북", "경남", "경기"
      ],
      publicAreaItems: [
        "10평대 이하", "10평대", "20평대", "30평대", "40평대", "그 이상"
      ],
      exclusiveAreaItems: [
        "10평대 이하", "10평대", "20평대", "30평대", "40평대", "그 이상"
      ],
      rentCostItems: [
        "5000만원 이하", "1억 이하", "1억대", "2억대", "3억대", "그 이상"
      ],
      spaceTypeItems: [
        "좌석형", "입식형"
      ],
      vacantRoomCountItems: [
        "5개 이하", "10개 이하", "20개 이하"
      ],
      spaceInfos: [
        {
            name: "a",
            region: "1",
            exclusiveArea: "1",
            publicArea: "1",
            rentCost: "2",
            spaceType: "3",
            vacantRoomCount: "4",
            score: "5",
            contactNum: "6",
            homepageUrl: "7",
        },
        {
          name: "b",
          region: "1",
          exclusiveArea: "1",
          publicArea: "1",
          rentCost: "2",
          spaceType: "3",
          vacantRoomCount: "4",
          score: "5",
          contactNum: "7",
          homepageUrl: "8"
        },
        {
          name: "c",
          region: "1",
          exclusiveArea: "1",
          publicArea: "1",
          rentCost: "2",
          spaceType: "3",
          vacantRoomCount: "4",
          score: "5",
          contactNum: "7",
          homepageUrl: "8"
        },
        ],
    }),

    methods: {
      search() {
        // axios 요청 후 데이터 교체 필요
        this.filterOptions.region = "서울";
        axios.get(`http://127.0.0.1/item?region=${this.filterOptions.region}`, headers)
        .then((data) => {
          this.changeData(data);
        })
        .catch((error) => {
          alert(error);
        })
      },
      changeData(newSpaceInfos) {
        this.spaceInfos = newSpaceInfos;
      }
    }
  }
</script>
