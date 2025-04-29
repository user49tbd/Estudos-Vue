<template>
  <footer class="footerC">
    <div class="content1">
      <h4>project01</h4>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat eum
        temporibus dignissimos commodi tempore. Veritatis eum quos minus sequi
        accusantium exercitationem magni sed quisquam illo, et alias. Veritatis,
        inventore atque.
      </p>
      <div class="imgs">
        <img src="/assets/icons/facebook.png" />
        <img src="/assets/icons/social.png" />
        <img src="/assets/icons/twitter.png" />
      </div>
      <p>&copy;example&trade;</p>
    </div>
    <div class="content2">
        <table>
            <thead>
                <tr>
                    <th>Links</th><th>Data</th><th>Objects</th>
                </tr>
            </thead>
            <tbody>
                <tr><td>link1</td><td>dataMain</td><td>obj1</td></tr>
                <tr><td>section</td><td>main</td><td>shape</td></tr>
                <tr><td>other</td><td>database</td><td>format</td></tr>
                <tr><td>search</td><td>topics</td><td>size</td></tr>
                <tr><td>info</td><td>data</td><td>obj</td></tr>
            </tbody>
        </table>
    </div>
  </footer>
</template>
<script>
export default {
  name: "Footer",
  data() {
    return {};
  },
};
</script>
<style scoped>
.footerC {
  width: 100%;
  height: 50vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  color: white;
  padding: 20px;
}
.content1 {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 30%;
  height: 100%;
  flex-direction: column;
  overflow: hidden;
  gap: 5px;
  padding: 20px;
}
.content1 > h4 {
  font-size: 50px;
  font-weight: bolder;
  font-family: Arial;
  text-transform: uppercase;
  border-left: 4px solid orange;
}
.content1 > p {
  font-size: 12px;
  font-family: Arial;
  text-align: justify;
}
.content2 {
  display: flex;
  align-items: flex-start;
  align-content: center;
  width: 70%;
  height: 100%;
}
.imgs{
    width: 100%;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    gap: 10px;
}
.imgs > img{
    height: 100%;
    aspect-ratio: 1/1;
    object-fit: cover;
    object-position: center;
    filter: invert(1);

}
table,thead,tbody,tr,td,th{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
}
table{
    height: 100%;
    table-layout: fixed;
    flex-direction: column;
    justify-content: flex-start;
}
tbody{
    justify-content: flex-start;
    flex-direction: column;
}
th{
    height: 50px;
    font-size: 40px;
    text-transform: uppercase;
}
td{
    height: 30px;
}

</style>
