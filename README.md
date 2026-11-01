package com.hkpools.analyzer

data class DataModel(
    val hari: String,
    val tanggal: String,
    val hasil: String
)
package com.hkpools.analyzer

import android.view.LayoutInflater
import android.view.ViewGroup
import androidx.recyclerview.widget.RecyclerView
import com.hkpools.analyzer.databinding.ItemRowBinding

class DataAdapter : RecyclerView.Adapter<DataAdapter.ViewHolder>() {

    private val list = mutableListOf<DataModel>()

    fun setData(data: List<DataModel>) {
        list.clear()
        list.addAll(data)
        notifyDataSetChanged()
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val binding = ItemRowBinding.inflate(
            LayoutInflater.from(parent.context), parent, false
        )
        return ViewHolder(binding)
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        holder.bind(list[position])
    }

    override fun getItemCount(): Int = list.size

    inner class ViewHolder(private val binding: ItemRowBinding) :
        RecyclerView.ViewHolder(binding.root) {
        fun bind(item: DataModel) {
            binding.tvHari.text = item.hari
            binding.tvTanggal.text = item.tanggal
            binding.tvHasil.text = item.hasil
        }
    }
}
package com.hkpools.analyzer

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.hkpools.analyzer.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding
    private val adapter = DataAdapter()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        setupRecyclerView()
        loadData()
    }

    private fun setupRecyclerView() {
        binding.recyclerView.adapter = adapter
    }

    private fun loadData() {
        val data = listOf(
            DataModel("SELASA", "31 Oktober 2023", "2946"),
            DataModel("SENIN", "30 Oktober 2023", "4514"),
            DataModel("MINGGU", "29 Oktober 2023", "6152"),
            DataModel("SABTU", "28 Oktober 2023", "2849"),
            DataModel("JUMAT", "27 Oktober 2023", "5480"),
            DataModel("KAMIS", "26 Oktober 2023", "7970")
        )
        adapter.setData(data)
    }
}
