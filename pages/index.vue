
<template>
  <div class="container p-6 mx-auto">
    <div class="container flex flex-wrap justify-between p-6 mx-auto mt-6">
      <h4 class="text-2xl font-bold text-black" data-cy="activity-title">Activity</h4>
      <button type="button" class="flex px-8 py-3 text-lg font-medium text-center text-white rounded-full bg-sky-500"
        data-cy="activity-add-button" @click="storeActivity()"> <span><img src="/assets/icons/icon-plus.svg"
            alt=""></span> Tambah</button>
    </div>

    <p v-if="$fetchState.pending" >Fetching activity...</p>
    <div v-else class="flex flex-wrap -mx-1 lg:-mx-4">
      <div class="w-full px-1 my-1 md:w-1/2 lg:my-4 lg:px-4 lg:w-1/4" data-cy="activity-item" v-for="activity in activities" :key="activity.id">
        <div class="p-6 bg-white border border-gray-200 rounded-lg shadow-md ">
          <NuxtLink :to="{name: 'detail', params:{id:activity.id} }">
            <div class="h-32">
              <h5 class="mb-2 text-xl font-semibold " data-cy="activity-item-title">{{ activity.title }}</h5>
            </div>
          </NuxtLink>
          <div class="flex justify-between activity-card-footer">
            <p class="mb-3 font-normal text-gray-500 dark:text-gray-400" data-cy="activity-date">
              {{ activity.created_at }}</p>
            <button data-cy="activity-item-delete-button" data-modal-target="modal-delete" data-modal-toggle="modal-delete" type="button" @click="openModalDelete(activity)">
              <img src="/assets/icons/activity-item-delete-button.svg" alt=""></button>
          </div>
        </div>
      </div>
      <!-- <ModalDelete 
        :id = modalDelete.id
        :title = modalDelete.title
      /> -->
    </div>
    <!-- <div v-else>
      <IllustrationAdd />
    </div> -->
  </div>
</template>

<script>
export default {
  data(){
    return{
      activities:[],
    }
  },

  async fetch(){
    this.activities = await this.$axios.get('/activity-groups?email=ulhaqitcom@gmail.com')
  },
}
</script>