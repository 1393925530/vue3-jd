<template>
  <div class="wrapper">
    <img
      src="http://www.dell-lee.com/imgs/vue3/user.png"
      alt=""
      class="wrapper__img"
    />
    <div class="wrapper__input">
      <input
        type="text"
        placeholder="请输入用户名"
        v-model="username"
        class="wrapper__input__content"
      />
    </div>
    <div class="wrapper__input">
      <input
        type="password"
        placeholder="请输入密码"
        v-model="password"
        autocomplete="new-password"
        class="wrapper__input__content"
      />
    </div>
    <div class="wrapper__input">
      <input
        type="password"
        placeholder="确认密码"
        v-model="ensurement"
        autocomplete="new-password"
        class="wrapper__input__content"
      />
    </div>
    <div class="wrapper__register-button" @click="handleRegister">
      注册
    </div>
    <div class="wrapper__register-link" @click="handleLoginClick">
      已有帐号去登陆
    </div>
    <Toast v-if="show" :message="toastMessage" />
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import { useRouter } from 'vue-router'
import { post } from '../../utils/request'
import Toast, { UseToastEffect } from '../../components/Toast'

const useRegisterEffect = showToast => {
  const router = useRouter()

  const data = reactive({
    username: '',
    password: '',
    ensurement: ''
  })

  const handleRegister = async () => {
    try {
      const result = await post('/api/user/login', {
        username: data.username,
        password: data.password
      })
      if (result?.errno === 0) {
        router.push({ name: 'Login' })
      } else {
        showToast('注册失败')
      }
    } catch (e) {
      showToast('请求失败')
    }
  }

  const { username, password, ensurement } = toRefs(data)

  return {
    username,
    password,
    ensurement,
    handleRegister
  }
}

const useLoginEffect = () => {
  const router = useRouter()

  const handleLoginClick = () => {
    router.push({ name: 'Login' })
  }

  return { handleLoginClick }
}

export default {
  name: 'Register',

  components: { Toast },

  setup () {
    const { show, toastMessage, showToast } = UseToastEffect()

    const {
      username,
      password,
      ensurement,
      handleRegister
    } = useRegisterEffect(showToast)

    const { handleLoginClick } = useLoginEffect()

    return {
      username,
      password,
      ensurement,
      handleRegister,
      show,
      toastMessage,
      handleLoginClick
    }
  },

  watch: {},

  computed: {},

  mounted () {},

  methods: {}
}
</script>

<style lang="scss" scoped>
@import '../../style/variables.scss';

.wrapper {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  transform: translateY(-50%);
  &__img {
    display: block;
    margin: 0 auto 0.4rem auto;
    width: 0.66rem;
    height: 0.66rem;
  }
  &__input {
    height: 0.48rem;
    margin: 0 0.4rem 0.16rem 0.4rem;
    padding: 0 0.16rem;
    background: #f9f9f9;
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 6px;
    &__content {
      line-height: 0.48rem;
      border: none;
      outline: none;
      width: 100%;
      background: none;
      font-size: 0.16rem;
      color: $content-notice-fontcolor;
      &::placeholder {
        color: $content-notice-fontcolor;
      }
    }
  }
  &__register-button {
    margin: 0.32rem 0.4rem 0.16rem 0.4rem;
    line-height: 0.48rem;
    background: $btn-bgColor;
    box-shadow: 0 0.04rem 0.08rem 0 rgba(0, 145, 255, 0.32);
    border-radius: 0.04rem;
    color: $bgColor;
    font-size: 0.16rem;
    text-align: center;
  }
  &__register-link {
    text-align: center;
    font-size: 0.14rem;
    color: $content-notice-fontcolor;
  }
}
</style>
