<script lang="ts">
const shuffleMembers = (
  members: Member[],
  pinTheFirstMember = false
): void => {
  let offset = pinTheFirstMember ? 1 : 0
  // `i` is between `1` and `length - offset`
  // `j` is between `0` and `length - offset - 1`
  // `offset + i - 1` is between `offset` and `length - 1`
  // `offset + j` is between `offset` and `length - 1`
  let i = members.length - offset
  while (i > 0) {
    const j = Math.floor(Math.random() * i)
    ;[members[offset + i - 1], members[offset + j]] = [
      members[offset + j],
      members[offset + i - 1]
    ]
    i--
  }
}
</script>

<script setup lang="ts">
import { VTLink } from '@vue/theme'
import membersCoreData from './members-core.json'
import membersEmeritiData from './members-emeriti.json'
import membersPartnerData from './members-partner.json'
import TeamHero from './TeamHero.vue'
import TeamList from './TeamList.vue'
import type { Member } from './Member'
shuffleMembers(membersCoreData as Member[], true)
shuffleMembers(membersEmeritiData as Member[])
shuffleMembers(membersPartnerData as Member[])
</script>

<template>
  <div class="TeamPage">
    <TeamHero>
      <template #title>Ekiple Tanışın</template>
      <template #lead>
        Vue ve ekosisteminin geliştirilmesi, bazıları
        <span class="nowrap">aşağıda yer alan</span>
        uluslararası bir ekip tarafından yönlendirilmektedir.
      </template>

      <template #action>
        <VTLink
          href="https://github.com/vuejs/governance/blob/master/Team-Charter.md"
        >
          Ekipler hakkında daha fazla bilgi
        </VTLink>
      </template>
    </TeamHero>

    <TeamList :members="(membersCoreData as Member[])">
      <template #title>Çekirdek Ekip Üyeleri</template>
      <template #lead>
        Çekirdek ekip üyeleri, bir veya daha fazla çekirdek projenin
        bakımında aktif olarak görev alan kişilerdir. Vue ekosistemine
        önemli katkılar sağlamışlardır ve projenin ve kullanıcılarının
        başarısına uzun vadeli bir bağlılık gösterirler.
      </template>
    </TeamList>

    <TeamList :members="(membersEmeritiData as Member[])">
      <template #title>Onursal Çekirdek Ekip Üyeleri</template>
      <template #lead>
        Burada, geçmişte değerli katkılarda bulunmuş ancak artık aktif
        olmayan bazı çekirdek ekip üyelerini onurlandırıyoruz.
      </template>
    </TeamList>

    <TeamList :members="(membersPartnerData as Member[])">
      <template #title>Topluluk Ortakları</template>
      <template #lead>
        Vue topluluğunun bazı üyeleri, topluluğu o kadar zenginleştirmiştir
        ki özel olarak anılmayı hak ederler. Bu kilit ortaklarla daha yakın
        bir ilişki geliştirdik ve yaklaşan özellikler ile duyurular konusunda
        sıklıkla onlarla koordinasyon sağlıyoruz.
      </template>
    </TeamList>
  </div>
</template>

<style scoped>
.TeamPage {
  padding-bottom: 16px;
}

@media (min-width: 768px) {
  .TeamPage {
    padding-bottom: 96px;
  }
}

.TeamList + .TeamList {
  padding-top: 64px;
}
</style>
