<template>
  <template v-if="user">
    <van-cell title="昵称" is-link to="/user/edit/" :value="user.username"
              @click="toEdit('username','昵称',user.username)"/>
    <van-cell title="帐号" :value="user.userAccount"/>

    <van-cell title="头像" is-link to="/user/editAvatar/" :value="user.avatarUrl"
              @click="toEditAvatar('avatarUrl','头像',user.avatarUrl)">
      <img style="height: 48px" :src="user.avatarUrl">
    </van-cell>
    <van-cell title="个性签名" is-link to="/user/edit/" :value="user.profile"
              @click="toEdit('profile','个性签名',user.profile)"/>
    <van-cell title="性别" is-link :value="user.gender ===0?'男':'女'"
              @click="toEditGender('gender','性别',user.gender ===0?'男':'女')"/>
    <van-cell title="电话" is-link to="/user/edit/" :value="user.phone" @click="toEdit('phone','电话',user.phone)"/>
    <van-cell title="邮箱" is-link to="/user/edit/" :value="user.email " @click="toEdit('email','邮箱',user.email)"/>
    <van-cell title="我的标签" is-link to="/user/editTags/"   @click="toEditTags('tags','标签',user.tags)"/>
    <van-cell title="注册时间" :value="dayjs(user.createTime).format('YYYY-MM-DD HH:mm:ss')"/>
  </template>



</template>

<script setup lang="ts">
import {useRouter} from "vue-router";
import {onMounted, ref} from "vue";
import {getCurrentUser} from "../services/user";
import * as dayjs from 'dayjs';


const user = ref();

onMounted(async () => {
  user.value = await getCurrentUser();

})

const router = useRouter();
const fileList = ref([]);


const toEdit = (editKey: string, editName: string, currentValue: string) => {
  router.push({
    path: '/user/edit',
    query: {
      editKey,
      editName,
      currentValue,
    }
  })
}

const toEditAvatar = (editKey: string, editName: string, currentValue: string) => {
  router.push({
    path: '/user/editAvatar',
    query: {
      editKey,
      editName,
      currentValue,
    }
  })
}

const toEditGender = (editKey: string, editName: string, currentValue: string) => {
  router.push({
    path: '/user/editGender',
    query: {
      editKey,
      editName,
      currentValue,
    }
  })
}

const toEditTags = (editKey: string, editName: string, currentValue: string) => {
  router.push({
    path: '/user/editTags',
    query: {
      editKey,
      editName,
      currentValue,
    }
  })
}


</script>

<style scoped>

</style>
