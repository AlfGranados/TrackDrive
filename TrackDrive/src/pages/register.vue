<script setup>
import AuthProvider from '@/views/pages/authentication/AuthProvider.vue'
import { useTheme } from 'vuetify'
import logo from '@images/favicon.ico'
import authV1MaskDark from '@images/pages/auth-v1-mask-dark.png'
import authV1MaskLight from '@images/pages/auth-v1-mask-light.png'
import authV1Tree2 from '@images/pages/auth-v1-tree-2.png'
import authV1Tree from '@images/pages/auth-v1-tree.png'

const form = ref({
  username: '',
  email: '',
  password: '',
  privacyPolicies: false,
})

const vuetifyTheme = useTheme()

const authThemeMask = computed(() => {
  return vuetifyTheme.global.name.value === 'light' ? authV1MaskLight : authV1MaskDark
})

const isPasswordVisible = ref(false)
</script>

<template>
  <div class="auth-wrapper d-flex align-center justify-center pa-4">
    <VCard
      class="auth-card pa-4 pt-7"
      max-width="448"
    >
      <VCardItem class="justify-center">
        <template #prepend>
          <div class="d-flex">
            <img src='@images/favicon.ico' alt="Logo" style="width: 30px; height: 30px;" />
          </div>
        </template>

        <VCardTitle class="font-weight-semibold text-2xl text-uppercase">
          TrackDrive
        </VCardTitle>
      </VCardItem>

      <VCardText class="pt-2">
        <h5 class="text-h5 font-weight-semibold mb-1">
          Registro de Usuario 🚀
        </h5>
        <p class="mb-0">
          Un mensaje o algo!
        </p>
      </VCardText>

      <VCardText>
        <VForm @submit.prevent="() => {}">
          <VRow>
            <!-- Username -->
            <VCol cols="12">
              <VTextField
                v-model="form.username"
                label="Nombre de Usuario"
              />
            </VCol>
            <!-- email -->
            <VCol cols="12">
              <VTextField
                v-model="form.email"
                label="Email"
                type="email"
              />
            </VCol>

            <!-- password -->
            <VCol cols="12">
              <VTextField
                v-model="form.password"
                label="Contraseña"
                :type="isPasswordVisible ? 'text' : 'password'"
                :append-inner-icon="isPasswordVisible ? 'mdi-eye-off-outline' : 'mdi-eye-outline'"
                @click:append-inner="isPasswordVisible = !isPasswordVisible"
              />
              <div class="d-flex align-center mt-1 mb-4">
                <VCheckbox
                  id="privacy-policy"
                  v-model="form.privacyPolicies"
                  inline
                />
                <VLabel
                  for="privacy-policy"
                  style="opacity: 1;"
                >
                  <span class="me-1">Acepto la </span>
                  <a
                    href="javascript:void(0)"
                    class="text-primary"
                  >política de privacidad y términos.</a>
                </VLabel>
              </div>

              <VBtn
                block
                type="submit"
                to="/"
              >
                Sign up
              </VBtn>
            </VCol>

            <!-- login instead -->
            <VCol
              cols="12"
              class="text-center text-base"
            >
              <span>Ya tiene una cuenta?</span>
              <RouterLink
                class="text-primary ms-2"
                to="login"
              >
                Inicie sesión
              </RouterLink>
            </VCol>

          </VRow>
        </VForm>
      </VCardText>
    </VCard>
    <!--    <VImg -->
    <!--      class="auth-footer-start-tree d-none d-md-block" -->
    <!--      :src="authV1Tree" -->
    <!--      :width="250" -->
    <!--    /> -->

    <!--    <VImg -->
    <!--      :src="authV1Tree2" -->
    <!--      class="auth-footer-end-tree d-none d-md-block" -->
    <!--      :width="350" -->
    <!--    /> -->

    <!-- bg img -->
    <VImg
      class="auth-footer-mask d-none d-md-block"
      :src="authThemeMask"
    />
  </div>
</template>

<style lang="scss">
@use "@core/scss/pages/page-auth.scss";
</style>
